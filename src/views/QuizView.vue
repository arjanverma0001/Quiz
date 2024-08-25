<script setup>
    import Question from '@/components/Question.vue';
    import QuestionHeader from '@/components/QuestionHeader.vue';
    import Result from '@/components/Result.vue';
    import { computed, ref } from 'vue';
    import { useRoute } from 'vue-router';
    import quizes from '@/data/quizes.json';

    const route = useRoute();
    const quizId = parseInt(route.params.id);
    const currentQuestionIndex = ref(0);
    const numberOfCorrectAnswers = ref(0);
    const showResults = ref(false);
    const quiz = quizes.find(q => q.id === quizId);
    const questionStatus = computed(()=>`${currentQuestionIndex.value}/${quiz.questions.length}`);
    const barPercentage = computed(()=> `${currentQuestionIndex.value/quiz.questions.length*100}%`);

    function onOptionSelected(isCorrect){
        if(isCorrect){
            numberOfCorrectAnswers.value++;
        }
        if(quiz.questions.length -1 === currentQuestionIndex.value){
            showResults.value = true;
        }
        currentQuestionIndex.value++;
    }

</script>

<template>
    <div class="container">
        <QuestionHeader 
        :questionStatus="questionStatus" 
        :barPercentage="barPercentage"
        />
        <Question 
        :question="quiz.questions[currentQuestionIndex]" 
        @selectOption="onOptionSelected"
        v-if="!showResults"
        />
        <Result 
        :numberOfCorrectAnswers="numberOfCorrectAnswers"  
        :quizQuestionLength="quiz.questions.length"
        v-else
        />
    </div>
</template>

<style>
  .container{
    max-width: 1000px;
    margin: 0 auto;
  }
</style>
