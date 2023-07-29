<template>
        <h2>Products Page</h2>
        <div class="row">
                <div class="col-3"></div>
                <div class="col-6"></div>
                <div class="col-3">
                     <SearchTextBox @searchInput="inputHandler"></SearchTextBox>
                </div>
        </div>
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
   import {ref, reactive, onMounted} from 'vue'
   import SearchTextBox from '../components/SearchTextBox.vue';
    //ajax
    //XMLHttpRequest、fetch
    //jQuery $.ajax() $.get()....
    //axios
    const keyword = ref("")
   const products = ref([])
    const loadProducts = async ()=>{
       
      const response = await fetch(`https://localhost:7192/api/Products?keyword=${keyword.value}`)
      const datas = await response.json()
      products.value = datas
      console.log(products.value)
    }

    //這個方法是由子元件引發searchInput事件後執行的
    const inputHandler = value=>{
        keyword.value = value
        loadProducts()
    }
    onMounted(()=>{
         loadProducts()
    })
   
</script>
    
<style>
    
</style>