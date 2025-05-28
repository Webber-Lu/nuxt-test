<!-- components/EquipmentStatus.vue -->
<template>
  <div class="equipment-status">
    <div
      class="status-indicator"
      :class="statusClass"
      :style="statusStyle"
    >
      {{ equipment.name }}
    </div>
    <div class="status-text" :style="{ color: statusColor }">
      {{ equipment.status }}
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  equipment: {
    type: Object,
    required: true
  }
})

// 動態類別計算
const statusClass = computed(() => ({
  'status-available': props.equipment.status === '可用',
  'status-maintenance': props.equipment.status === '維修中',
  'status-borrowed': props.equipment.status === '已借出'
}))

// 動態樣式計算
const statusColor = computed(() => {
  switch(props.equipment.status) {
    case '可用': return '#27ae60'
    case '維修中': return '#e74c3c'
    case '已借出': return '#f39c12'
    default: return '#95a5a6'
  }
})

const statusStyle = computed(() => ({
  borderLeftColor: statusColor.value,
  borderLeftWidth: '4px'
}))
</script>

<style scoped>
.equipment-status {
  background: white;
  border-radius: 6px;
  padding: 16px;
  margin: 8px 0;
  border-left: 4px solid #ddd;
  transition: all 0.3s ease;
}

.status-indicator {
  font-weight: 500;
  margin-bottom: 8px;
}

.status-available {
  background-color: #d5f4e6;
}

.status-maintenance {
  background-color: #ffeaea;
}

.status-borrowed {
  background-color: #fff3cd;
}
</style>