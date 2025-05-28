    <!-- pages/equipment/index.vue -->
<template>
  <div>
    <h1>設備管理</h1>
    <div class="equipment-list">
      <div class="equipment-card" v-for="item in equipment" :key="item.id">
        <h3>{{ item.name }}</h3>
        <p>編號：{{ item.id }}</p>
        <p>狀態：{{ item.status }}</p>
        <NuxtLink :to="`/equipment/${item.id}`">查看詳情</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const equipment = [
  { id: 'OSC001', name: '數位示波器', status: '可用' },
  { id: 'GEN002', name: '函數產生器', status: '維修中' },
  { id: 'PSU003', name: '直流電源供應器', status: '可用' }
]
</script>

<style scoped>
.equipment-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.equipment-card {
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.equipment-card a {
  display: inline-block;
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #27ae60;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}
</style>