<template>
  <div>
    <h1>專案管理</h1>
    <div class="projects-list">
      <div class="project-card" v-for="project in projects" :key="project.id">
        <h3>{{ project.name }}</h3>
        <p>專案編號：{{ project.id }}</p>
        <p>負責人：{{ project.owner }}</p>
        <NuxtLink :to="`/projects/${project.id}`">查看詳情</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const projects = [
  { id: 'P001', name: '智慧教室系統', owner: '王大明' },
  { id: 'P002', name: '自動化測試平台', owner: '李小華' },
  { id: 'P003', name: '雲端儲存服務', owner: '張小美' }
]
</script>

<style scoped>
.projects-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.project-card {
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.project-card a {
  display: inline-block;
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #2980b9;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}
</style>