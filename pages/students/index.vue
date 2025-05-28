<!-- pages/students/index.vue -->
<template>
  <div>
    <h1>學生管理</h1>

    <div class="search-section">
      <input
        v-model="searchQuery"
        placeholder="搜尋學生姓名或學號"
        @keyup.enter="searchStudents"
      >
      <button @click="searchStudents">搜尋</button>
    </div>

    <div class="students-grid">
      <div
        v-for="student in filteredStudents"
        :key="student.id"
        class="student-card"
        @click="viewStudent(student.id)"
      >
        <h3>{{ student.name }}</h3>
        <p>學號：{{ student.id }}</p>
        <p>年級：{{ student.grade }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const searchQuery = ref('')

const students = [
  { id: 'E1001', name: '張小明', grade: '大四' },
  { id: 'E1002', name: '李小華', grade: '大三' },
  { id: 'E1003', name: '王小美', grade: '大二' }
]

const filteredStudents = computed(() => {
  if (!searchQuery.value) return students
  return students.filter(student =>
    student.name.includes(searchQuery.value) ||
    student.id.includes(searchQuery.value)
  )
})

const searchStudents = () => {
  // 搜尋邏輯已在 computed 中處理
  console.log('搜尋:', searchQuery.value)
}

const viewStudent = (studentId) => {
  // 程式化導航
  navigateTo(`/students/${studentId}`)
}
</script>

<style scoped>
.search-section {
  margin: 20px 0;
}

.search-section input {
  padding: 10px;
  width: 300px;
  margin-right: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.search-section button {
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.students-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 15px;
  margin-top: 20px;
}

.student-card {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
}

.student-card:hover {
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  transform: translateY(-2px);
}
</style>