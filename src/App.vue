<script setup>
import Nav from './componnets/Nav.vue'
import Home from './views/Home/Home.vue'
</script>

<template>
  <div class="main">
    <Nav />
    <div class="content-container">
      <router-view></router-view />
    </div>
  </div>
</template>

<style scoped>
.content-container {
  margin-top: 61px;
  background-color: #f5f5f5;
}
</style>
