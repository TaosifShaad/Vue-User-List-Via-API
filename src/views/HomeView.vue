<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/favicon.png">
    <div class="list">
        <UserCard v-for="user in userList" :key="user.id" :result="user"></UserCard>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import {reactive, toRefs} from 'vue';
import UserCard from '@/components/UserCard.vue';

export default {
  name: 'HomeView',
  components: {
    UserCard
  },
  setup() {
    const state = reactive({
      userList: [],
    });

    async function getData() {
        const res = await fetch('https://randomuser.me/api/?results=25');
        const finalRes = await res.json();
        state.userList = finalRes.results;
        console.log(state.userList);
    }

    getData();

    return {
      ...toRefs(state),
    }
  }
}
</script>

<style scoped>
.home {
  padding: 0px 30px 30px;
}
.list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 30px;
  row-gap: 70px;
}

img {
  width: 200px;
  margin-block-end: 40px;
}
</style>
