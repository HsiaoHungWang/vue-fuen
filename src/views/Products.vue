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
        <nav aria-label="Page navigation example">
  <ul class="pagination">   
    <li class="page-item" v-for="(value, index) in totalPages" :key="index" @click="clickHandler(value)">
        <a :class="{'currentPage':thePage===value, 'page-link':true}">{{ value }}</a></li>   
  </ul>
</nav>
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
   const totalPages = ref(1)  //共幾頁
   const thePage = ref(1)  //第幾頁
   const API = import.meta.env.VITE_API_URL
    const loadProducts = async ()=>{
       
      const response = await fetch(`${API}Products?keyword=${keyword.value}&page=${thePage.value}&pageSize=3`)
      const datas = await response.json()
      products.value = datas.products
      console.log(products.value)
      totalPages.value = datas.totalPages
    }

    //這個方法是由子元件引發searchInput事件後執行的
    const inputHandler = value=>{
        keyword.value = value
        loadProducts()
    }

    //分頁
    const clickHandler=(page)=>{
        thePage.value = page
        loadProducts()
    }
    onMounted(()=>{
         loadProducts()
    })
   
</script>
    
<style scoped>
    .currentPage{
        background-color: lightgray;
    }
    .pagination li{
        cursor: pointer;
    }
</style>