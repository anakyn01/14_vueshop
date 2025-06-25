<template>
  <div class="product-list">
    <h1>상품 목록</h1>
    <div v-if="loading">로딩 중...</div>
    <div v-else class="product-grid">
      <div v-for="product in products" :key="product.id" class="product-card">
        <img :src="product.image" :alt="product.title" />
        <h2>{{ product.title }}</h2>
        <p>₩{{ (product.price * 1200).toLocaleString() }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ProductList',
  data() {
    return {
      products: [],
      loading: true
    }
  },
  mounted() {
    axios.get('https://fakestoreapi.com/products')
      .then(res => {
        this.products = res.data
      })
      .catch(err => {
        console.error('API 에러:', err)
      })
      .finally(() => {
        this.loading = false
      })
  }
}
</script>

<style scoped>
.product-list {
  max-width: 100%;
  margin: auto;
  padding: 20px;
}

.product-grid {
  width:1200px;
  max-width:100%;
  flex-wrap: wrap;
  display: flex;
  gap: 20px;
  justify-content: center;
}

.product-card {
  width: 200px;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 12px;
  text-align: center;
  background-color: #fff;
  transition: box-shadow 0.2s ease;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.product-card img {
  max-width: 100%;
  height: 180px;
  object-fit: contain;
  margin-bottom: 10px;
}
</style>
