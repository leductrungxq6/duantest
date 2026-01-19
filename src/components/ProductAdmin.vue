// src/views/ProductAdmin.vue
<template>
  <div class="admin">
    <h2>Quản lý Sản phẩm</h2>

    <form class="form-add" @submit.prevent="addProduct">
      <input v-model="newProduct.name" type="text" placeholder="Tên sản phẩm" required />
      <input v-model.number="newProduct.price" type="number" placeholder="Giá" required />
      <input ref="fileInput" type="file" accept="image/*" @change="handleImage" required />
      <input v-model="newProduct.category" type="text" placeholder="Danh mục" required />
      <button type="submit">Thêm sản phẩm</button>
    </form>

    <table>
      <thead>
        <tr>
          <th>STT</th>
          <th>Tên sản phẩm</th>
          <th>Giá</th>
          <th>Hình ảnh</th>
          <th>Danh mục</th>
          <th>Hành động</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in products" :key="product.id">
          <td>{{ index + 1 }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}đ</td>
          <td><img :src="product.image" width="60" /></td>
          <td>{{ product.category }}</td>
          <td>
            <button @click="editProduct(product.id)">✏️</button>
            <button @click="deleteProduct(product.id)">🗑️</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const products = ref([
  { id: 1, name: 'Áo thun FPT', price: 150000, image: '/img/aothun.jpg', category: 'Áo' },
  { id: 2, name: 'Quần jeans', price: 250000, image: '/img/quan.jpg', category: 'Quần' }
])

const fileInput = ref(null)
const newProduct = ref({ name: '', price: '', image: '', category: '' })

const handleImage = (e) => {
  const file = e.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = (event) => {
      newProduct.value.image = event.target.result
    }
    reader.readAsDataURL(file)
  }
}

const addProduct = () => {
  if (newProduct.value.name && newProduct.value.price && newProduct.value.image && newProduct.value.category) {
    const newId = products.value.length ? products.value.at(-1).id + 1 : 1
    products.value.push({ id: newId, ...newProduct.value })
    newProduct.value = { name: '', price: '', image: '', category: '' }
    if (fileInput.value) fileInput.value.value = ''
  }
}

const editProduct = (id) => {
  alert('Sửa sản phẩm ID ' + id)
}

const deleteProduct = (id) => {
  if (confirm('Xóa sản phẩm?')) {
    const index = products.value.findIndex(p => p.id === id)
    products.value.splice(index, 1)
  }
}
</script>

<style scoped>
.admin {
  padding: 1rem;
}

.form-add {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 1.5rem;
}

.form-add input[type="text"],
.form-add input[type="number"],
.form-add input[type="file"] {
  padding: 8px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  flex: 1 1 200px;
}

.form-add button {
  background-color: #28a745;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
}

.form-add button:hover {
  background-color: #218838;
}

table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: left;
}
img {
  border-radius: 4px;
  object-fit: cover;
  height: 60px;
  width: 60px;
}
</style>
