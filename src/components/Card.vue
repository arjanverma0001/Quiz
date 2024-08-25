<script setup>
 import { defineProps } from 'vue';
 import { useRouter } from 'vue-router';

 const router = useRouter();

 defineProps({
    quizes :{
        type : Array
    }
 })
const NavigateToQuiz = (quiz) =>{
    router.push(`/quiz/${quiz.id}`);
}
</script>

<template>
    <div @click="NavigateToQuiz(quiz)" v-for="quiz in quizes" class="card" :key="quiz.id">
        <img :src="quiz.img" alt="">
        <div class="card-text">
            <h2>{{quiz.name}}</h2>
            <p>{{quiz.questions.length}} Questions in the quiz</p>
        </div>
    </div>
</template>

<style scoped>
/* Card style */

.card{
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
  }
  .card img {
    width: 100%;
    height: 190px;
    margin: 0;
  }
  .card-text{
    padding: 0 5px;
  }
  .card .card-text h2{
    font-weight: bold;
  }
</style>
