<template>
    <div v-if="state === 'loading'">Loading...</div>
    <div v-else-if="state === 'error'">Error loading quiz</div>
    <div v-else>

    <Quiz :quiz="quiz" v-if="quiz" />
         <!-- <div v-for="question in quiz.questions" :key="question.id">
            <h2>{{ question.title }}</h2>
            <ul>
                <li v-for="answer in question.answers" :key="answer.id">
                    <input type="radio" :name="question.id" :value="answer.id">
                    <label>{{ answer.text }}</label>
                </li>
            </ul>
        </div> -->

    </div>
</template>


<script setup>
import { onMounted } from 'vue';
import { ref } from 'vue';
import Quiz from './components/Quiz.vue';
const quiz = ref(null);
const state = ref('loading');

onMounted(() => {
    fetch('/quiz.json')
        .then(response => response.json())
        .then(data => {

            quiz.value = data
            state.value = 'loaded'
        }
        ).catch(() => {
            state.value = 'error'
        });
})
</script>