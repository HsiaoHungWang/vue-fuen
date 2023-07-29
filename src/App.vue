<script setup>
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.js'
import 'bootstrap-icons/font/bootstrap-icons.css'
import Navbar from './components/Navbar.vue'
</script>

<template>
  <div class="container">
    <Navbar class="mb-3"></Navbar>
  <h2>Hello Vue!!</h2>
  <router-view />
  </div>

</template>

<style scoped>
</style>
