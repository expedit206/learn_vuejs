<template>

    <label :for="id" :class="classes">
        <input :disabled="answer" :id="id" type="radio" name="answer" v-model="answer" :value="value" @change="onChange">

        <!-- {{ classes.right }} -->
        {{ value }}
    </label>

</template>

<script setup>
import { computed, ref, watch } from 'vue';

const props = defineProps({
    id: Number,
    value : String,
    correctAnswer : String
})

const emits = defineEmits(['change'])

const onChange = (e)=>{
    emits('change', e)
}

const answer =defineModel()

const classes = computed(()=>(
    {right: answer.value && props.value === props.correctAnswer,
    wrong: answer.value && answer.value !== props.correctAnswer && answer.value===props.value}
))

// watch(classes, ()=> console.log(classes))
console.log(answer.value);


</script>

<style>
.right{
    color:green
}
.wrong{
    color:red
}
</style>