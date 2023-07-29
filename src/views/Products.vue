<template>
        <h2>Products Page</h2>
        <table class="table table-bordered">
                <thead>
                        <tr>
                                <th>產品編號</th>
                                <th>產品名稱</th>
                                <th>產品價格</th>
                                <th>庫存量</th>
                        </tr>
                </thead>
                <tbody>
                        <tr v-for="product in products" :key="product.id">
                        <td>{{ product.id }}</td>
                        <td>{{ product.name }}</td>
                        <td>{{ product.price}}</td>
                        <td>{{ product.stock }}</td>
                        </tr>
                </tbody>
        </table>
</template>
    
<script setup>
   import {ref, reactive} from 'vue'
    //ajax
    //XMLHttpRequest、fetch
    //jQuery $.ajax() $.get()....
    //axios
   const products = ref([])

    const loadProducts = async ()=>{
      const response = await fetch('https://localhost:7192/api/Products')
      const datas = await response.json()
      products.value = datas
      console.log(products.value)
    }
    loadProducts()
</script>
    
<style>
    
</style>