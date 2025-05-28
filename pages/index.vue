<!-- pages/index.vue -->
<template>
  <div>
    <h1>歡迎來到電機系實驗室管理系統</h1>
    <p>選擇下列功能：</p>
    <nav>
      <ul>
        <li><NuxtLink to="/equipment">設備管理</NuxtLink></li>
        <li><NuxtLink to="/students">學生管理</NuxtLink></li>
        <li><NuxtLink to="/projects">專題管理</NuxtLink></li>
      </ul>
    </nav>
  </div>
</template>

<style scoped>
nav ul {
  list-style: none;
  padding: 0;
}

nav li {
  margin: 10px 0;
}

nav a {
  display: inline-block;
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 5px;
}

nav a:hover {
  background-color: #2980b9;
}
</style>