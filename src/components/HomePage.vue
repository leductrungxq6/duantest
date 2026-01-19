<template>
  <div class="home">
    <h2 class="heading">🛒 Sản phẩm mới nhất</h2>
    <div class="product-list">
      <div class="product" v-for="product in products" :key="product.id">
        <img :src="product.image" alt="Sản phẩm" />
        <h3>{{ product.name }}</h3>
        <p>{{ product.price.toLocaleString() }}đ</p>
        <button @click="addToCart(product)">Thêm vào giỏ</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  addToCart: Function
})

const products = ref([
  { id: 1, name: 'Áo thun FPT', price: 150000, image: '/img/aothun.jpg' },
  { id: 2, name: 'Quần jeans', price: 250000, image: '/img/quan.jpg' }
])
</script>

<style scoped>
.home {
  text-align: center;
}

.heading {
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
  color: #333;
}

.product-list {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.product {
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 15px;
  width: 220px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: white;
  transition: transform 0.2s ease;
}

.product:hover {
  transform: translateY(-5px);
}

.product img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 6px;
}

.product h3 {
  font-size: 1.1rem;
  margin: 10px 0 5px;
}

.product p {
  color: #555;
  margin-bottom: 10px;
}

.product button {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  margin-top: 5px;
}

.product button:hover {
  background-color: #36956e;
}
</style>
