<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/favicon.png">
    <div class="list" ref="scrollComponent">
        <UserCard v-for="user in userList" :key="user.id" :result="user"></UserCard>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import {reactive, toRefs, onMounted, onUnmounted} from 'vue';
import UserCard from '@/components/UserCard.vue';

export default {
  name: 'HomeView',
  components: {
    UserCard
  },
  setup() {
    const state = reactive({
      scrollComponent : null,
      userList: [],
    });

    async function getData(number) {
        let apiString = 'https://randomuser.me/api/?results=' + number;
        const res = await fetch(apiString);
        const finalRes = await res.json();
        // state.userList = finalRes.results;
        console.log(finalRes);
        finalRes.results.map(el => state.userList.push(el));
    }

    getData(8);

    onMounted(() => {
      window.addEventListener("scroll", handleScroll)
    })
    onUnmounted(() => {
      window.removeEventListener("scroll", handleScroll)
    })
    
    const handleScroll = () => {
      // let element = state.scrollComponent;
      // if (element.getBoundingClientRect().bottom < window.innerHeight) {
      //   getData(4);
      // }

      let bottomOfWindow = parseInt(document.documentElement.scrollTop + window.innerHeight + 1) === parseInt(document.documentElement.offsetHeight);
      if (bottomOfWindow) {
        getData(4);
      }
      console.log('scroltop' + document.documentElement.scrollTop);
      console.log('innerheight' + window.innerHeight);
      console.log('offsetHeight-----' + document.documentElement.offsetHeight);
      console.log('-------' + bottomOfWindow);
      console.log('handle function called');
      console.log('sum-----' + parseInt(document.documentElement.scrollTop + window.innerHeight))
    }

    return {
      ...toRefs(state),
      handleScroll
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
