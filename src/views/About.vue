<template>
    <input type="text" v-model="message">
    <h2>{{ message }}</h2>
</template>
    
<script setup>
    import { ref } from 'vue'
    const message = ref("Hello About")
</script>
    
<style>
    
</style>