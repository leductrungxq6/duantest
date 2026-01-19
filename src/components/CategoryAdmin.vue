// src/views/CategoryAdmin.vue
<template>
  <div class="admin">
    <h2>Quản lý Danh mục</h2>

    <form class="form-add" @submit.prevent="addCategory">
      <input v-model="newCategory.name" type="text" placeholder="Tên danh mục" required />
      <button type="submit">Thêm danh mục</button>
    </form>

    <table>
      <thead>
        <tr>
          <th>STT</th>
          <th>Tên danh mục</th>
          <th>Hành động</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(category, index) in categories" :key="category.id">
          <td>{{ index + 1 }}</td>
          <td>{{ category.name }}</td>
          <td>
            <button @click="editCategory(category.id)">✏️</button>
            <button @click="deleteCategory(category.id)">🗑️</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const categories = ref([
  { id: 1, name: 'Áo' },
  { id: 2, name: 'Quần' }
])

const newCategory = ref({ name: '' })

const addCategory = () => {
  if (newCategory.value.name.trim()) {
    const newId = categories.value.length ? categories.value.at(-1).id + 1 : 1
    categories.value.push({ id: newId, name: newCategory.value.name })
    newCategory.value.name = ''
  }
}

const editCategory = (id) => {
  alert('Sửa danh mục ID ' + id)
}

const deleteCategory = (id) => {
  if (confirm('Xóa danh mục?')) {
    const index = categories.value.findIndex(c => c.id === id)
    categories.value.splice(index, 1)
  }
}
</script>

<style scoped>
.admin {
  padding: 1rem;
}

.form-add {
  display: flex;
  gap: 10px;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.form-add input {
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
</style>
