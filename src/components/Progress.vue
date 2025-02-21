<template>
<div>
Etape {{ value }} / {{ max }}
<progress :value="value" :max="max"></progress>

</div>
</template>

<script setup>
import { defineProps } from 'vue'
defineProps({
    value: Number,
    max: Number
})


</script>