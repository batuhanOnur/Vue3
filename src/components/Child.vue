<template>
    <span>this is child component {{ title }}</span>
</template>

<script setup>
import { defineExpose, defineProps } from 'vue';
defineProps(['title'])

const a = 1;

function log(){
    console.log('child function');
}

defineExpose({
    a,
    log
})

</script>