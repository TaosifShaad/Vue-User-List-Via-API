<template>
    <div id="card">
        <img class="userImg" :src="result.picture.large" alt="">
        <h2>{{ result.name.title + " " + result.name.first + " " + result.name.last}}</h2>
        <h4> age: {{ result.dob.age }} </h4>
        <hr>
        <p> <i> {{ result.location.city + ", " + result.location.country }} </i></p>
        <small> {{ result.email }} </small> <br>
        <small> {{ result.cell }} </small>
    </div>
</template>



<script>
export default {
    name: 'UserCard',
    props: {
        result: Object
    },
    setup () {
        

        return {}
    }
}
</script>



<style scoped>
#card {
    border-radius: 50px;
    background: linear-gradient(145deg, #d4d4d4, #fbfbfb);
    box-shadow:  20px 20px 60px #c8c8c8, -20px -20px 60px #ffffff;
    width: 300px;
    margin: auto;
    padding: 30px;
}

.userImg {
    border-radius: 50%;
    width: 200px;
    margin-bottom: 25px;
}
</style>