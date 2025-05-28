<!-- pages/projects/[id].vue -->
<template>
  <div>
    <h1>專題詳情</h1>
    <div v-if="project">
      <h2>{{ project.title }}</h2>
      <p><strong>負責學生：</strong>{{ project.student }}</p>
      <p><strong>指導教授：</strong>{{ project.advisor }}</p>
      <p><strong>進度：</strong>{{ project.progress }}%</p>

      <div class="progress-bar">
        <div
          class="progress-fill"
          :style="{ width: project.progress + '%' }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup>
const route = useRoute()

// 路由驗證：檢查專題 ID 格式
definePageMeta({
  validate: async (route) => {
    // 檢查 ID 是否為 P 開頭加上數字
    return typeof route.params.id === 'string' && /^P\d+$/.test(route.params.id)
  }
})

// 模擬專題資料
const projects = {
  'P001': {
    title: '智慧電網監控系統',
    student: '張小明',
    advisor: '李教授',
    progress: 75
  },
  'P002': {
    title: '無線感測網路設計',
    student: '王小華',
    advisor: '陳教授',
    progress: 60
  }
}

const project = computed(() => {
  return projects[route.params.id]
})
</script>

<style scoped>
.progress-bar {
  width: 100%;
  height: 20px;
  background-color: #ecf0f1;
  border-radius: 10px;
  overflow: hidden;
  margin-top: 15px;
}

.progress-fill {
  height: 100%;
  background-color: #27ae60;
  transition: width 0.3s ease;
}
</style>