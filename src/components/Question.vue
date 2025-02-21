<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in randomChoices" :key="index">
            <Answer :id="index" :answer="answer" :value="choice" v-model="answer" 
            :correctAnswer ="question.correct_answer" @change="onAnswer" />
                <!-- <label :for="index">
                <input :disabled="answer" :id="index" type="radio" name="answer" v-model="answer" :value ="choice">
                
                {{ choice }}
                </label> -->
            </li>
        </ul>
        {{ answer }}
        <!-- <button @click="emits('answer', answer)" :disabled="!answer">Question suivante</button> -->
    </div>
</template>

<script setup>
const props = defineProps({
    question: Object
})
import {computed, onMounted, ref} from 'vue'
import { randomArray } from './functions/array';
import Answer from './Answer.vue';
const emits = defineEmits(['answer']);
const answer =ref(null)

const randomChoices = computed(()=>randomArray(props.question.choices))

const onAnswer= ()=>{
clearTimeout(timer)
timer = setTimeout(() => {
    emits('answer', answer.value)
}, 1000);    
}
let timer

onMounted(()=>{
    timer = setTimeout(() => {
        answer.value = ''
        onAnswer()
    }, 3000);
})
</script>


