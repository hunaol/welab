<script setup>
import MainCard from './components/MainCard.vue'
</script>
<template>
  <div class="home-container">
    <div class="up-container">
      <div class="left-container">
        <MainCard class="main-card" />
      </div>
      <div class="right-container">
        这是右侧的内容
      </div>
    </div>

  </div>
</template>
<style scoped>
.home-container {
  height: 100vh;
  padding: 20px;
  background-color: #ccc;
}

.up-container {
  display: flex;
  justify-content: space-between;
}



.main-card {
  margin-left: 30px;
}
</style>
