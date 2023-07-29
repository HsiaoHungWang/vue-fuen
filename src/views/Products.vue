<template>
        <h2>Products Page</h2>
</template>
    
<script setup>
    //ajax
    //XMLHttpRequest、fetch
    //jQuery $.ajax() $.get()....
    //axios

    const loadProducts = async ()=>{
      const response = await fetch('https://localhost:7192/api/Products')
      const datas = await response.json()
      console.log(datas)
    }
    loadProducts()
</script>
    
<style>
    
</style>