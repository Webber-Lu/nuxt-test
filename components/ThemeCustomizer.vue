<!-- components/ThemeCustomizer.vue -->
<template>
  <div class="theme-panel">
    <h3>介面主題設定</h3>
    <div class="controls">
      <label>
        主色調：
        <input type="color" v-model="primaryColor">
      </label>
      <label>
        字體大小：
        <input type="range" v-model="fontSize" min="12" max="20">
      </label>
    </div>
    <div class="preview-text">
      電機工程系實驗室管理系統
    </div>
  </div>
</template>

<script setup>
const primaryColor = ref('#2c3e50')
const fontSize = ref(16)
</script>

<style scoped>
.theme-panel {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.preview-text {
  margin-top: 20px;
  padding: 15px;
  background-color: v-bind(primaryColor);
  color: white;
  font-size: v-bind(fontSize + 'px');
  border-radius: 4px;
  text-align: center;
}

.controls {
  display: flex;
  gap: 20px;
  margin: 15px 0;
}

.controls label {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
</style>