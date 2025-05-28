<!-- pages/equipment/[id].vue -->
<template>
  <div>
    <NuxtLink to="/equipment">← 返回設備列表</NuxtLink>

    <div v-if="equipment" class="equipment-detail">
      <h1>{{ equipment.name }}</h1>
      <div class="detail-grid">
        <div class="info-section">
          <h3>基本資訊</h3>
          <p><strong>設備編號：</strong>{{ equipment.id }}</p>
          <p><strong>型號：</strong>{{ equipment.model }}</p>
          <p><strong>製造商：</strong>{{ equipment.manufacturer }}</p>
          <p><strong>狀態：</strong>
            <span :class="statusClass">{{ equipment.status }}</span>
          </p>
        </div>

        <div class="specs-section">
          <h3>規格參數</h3>
          <ul>
            <li v-for="spec in equipment.specifications" :key="spec.name">
              <strong>{{ spec.name }}：</strong>{{ spec.value }}
            </li>
          </ul>
        </div>
      </div>

      <div class="actions">
        <button @click="borrowEquipment" :disabled="equipment.status !== '可用'">
          借用設備
        </button>
        <button @click="reportIssue">回報問題</button>
      </div>
    </div>

    <div v-else class="not-found">
      <h2>找不到設備</h2>
      <p>設備編號 "{{ route.params.id }}" 不存在</p>
    </div>
  </div>
</template>

<script setup>
const route = useRoute()

// 模擬設備資料庫
const equipmentDatabase = {
  'OSC001': {
    id: 'OSC001',
    name: '數位示波器',
    model: 'DS1054Z',
    manufacturer: 'Rigol',
    status: '可用',
    specifications: [
      { name: '頻寬', value: '50MHz' },
      { name: '取樣率', value: '1GSa/s' },
      { name: '通道數', value: '4' }
    ]
  },
  'GEN002': {
    id: 'GEN002',
    name: '函數產生器',
    model: 'DG1032Z',
    manufacturer: 'Rigol',
    status: '維修中',
    specifications: [
      { name: '頻率範圍', value: '1μHz - 30MHz' },
      { name: '波形', value: '正弦波、方波、三角波' },
      { name: '輸出電壓', value: '1mVpp - 10Vpp' }
    ]
  }
}

// 根據路由參數獲取設備資料
const equipment = computed(() => {
  return equipmentDatabase[route.params.id]
})

// 計算狀態樣式
const statusClass = computed(() => ({
  'status-available': equipment.value?.status === '可用',
  'status-maintenance': equipment.value?.status === '維修中',
  'status-borrowed': equipment.value?.status === '已借出'
}))

// 借用設備功能
const borrowEquipment = () => {
  alert(`已申請借用 ${equipment.value.name}`)
}

// 回報問題功能
const reportIssue = () => {
  alert('問題回報功能開發中...')
}

console.log('當前設備ID:', route.params.id)
</script>

<style scoped>
.equipment-detail {
  max-width: 800px;
  margin: 20px 0;
}

.detail-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin: 20px 0;
}

.info-section, .specs-section {
  background-color: #f8f9fa;
  padding: 20px;
  border-radius: 8px;
}

.specs-section ul {
  list-style: none;
  padding: 0;
}

.specs-section li {
  margin: 8px 0;
}

.status-available {
  color: #27ae60;
  font-weight: bold;
}

.status-maintenance {
  color: #e74c3c;
  font-weight: bold;
}

.status-borrowed {
  color: #f39c12;
  font-weight: bold;
}

.actions {
  margin-top: 30px;
}

.actions button {
  margin-right: 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.actions button:first-child {
  background-color: #3498db;
  color: white;
}

.actions button:last-child {
  background-color: #95a5a6;
  color: white;
}

.actions button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}

.not-found {
  text-align: center;
  padding: 40px;
  background-color: #f8f9fa;
  border-radius: 8px;
}
</style>