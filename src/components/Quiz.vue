<template>
<div>
<h1>
{{ quiz.title }}
<Progress :value="step"  :max="quiz.questions.length" />
<Question :key="question.question" :question="question" v-if="state == 'question'" @answer="addAnswer"></Question>
<Recap v-if="state== 'recap'" :answers="answers" :quiz="quiz" />
{{ answers }}
</h1>
</div>
</template>

<script setup>
import { ref } from 'vue'
import Progress from './Progress.vue'
import Question from './Question.vue'
import Recap from './Recap.vue'
import { defineProps, computed } from 'vue' 
// import { defineProps } from 'vue'
const props = defineProps({
    quiz: Object
})
const state = ref('question')
const answers= ref(props.quiz.questions.map(()=>null))
const step = ref(0)

const question = computed(() => {
    return props.quiz.questions  [step.value]
})

const addAnswer = (answer)=>{
    answers.value[step.value] = answer
    if(step.value === props.quiz.questions.length){
        state.value = 'recap';
    }else{
        step.value++
    }
}
</script>