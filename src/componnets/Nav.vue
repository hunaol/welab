<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import logo from "@/assets/img/welab.png"

const isScrolled = ref(false)

function handleScroll() {
  isScrolled.value = window.scrollY > 60
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>
<template>
  <div class="nav-container" :class="{ 'nav-glass': isScrolled }">
    <div class="logo" :class="{ 'logo-hide': isScrolled }">
      <img :src="logo" alt="welab" />
    </div>
    <ul class="nav">
      <li>
        <router-link to="/">首页</router-link>
      </li>
      <li>
        <router-link to="/about">成员展示</router-link>
      </li>
      <li>
        <router-link to="/contact">联系我们</router-link>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.nav-container {
  display: flex;
  height: 60px;
  width: 100%;
  justify-content: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;

  /* 初始态：轻微渐变 + 半透明白 + 轻模糊 */
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.55), rgba(240, 238, 255, 0.45));
  backdrop-filter: blur(6px) saturate(120%);
  -webkit-backdrop-filter: blur(6px) saturate(120%);
  border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.04);

  transition: background 0.35s ease, backdrop-filter 0.35s ease, box-shadow 0.35s ease, border-color 0.35s ease;
}

/* 滚动后：更通透 + 更强模糊 + 柔光边框 */
.nav-container.nav-glass {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.18), rgba(230, 225, 255, 0.12));
  backdrop-filter: blur(18px) saturate(160%);
  -webkit-backdrop-filter: blur(18px) saturate(160%);
  border-bottom: 1px solid rgba(255, 255, 255, 0.25);
  box-shadow: 0 4px 20px rgba(120, 100, 180, 0.1);
}

/* 导航链接统一深色，毛玻璃上清晰可读 */
.nav-container .nav li a,
.nav-container.nav-glass .nav li a {
  color: #2d2a3a;
}

.nav-container .logo {
  margin-left: 50px;
  width: 90px;
  height: 42px;
  margin-top: 9px;
  border-radius: 10px;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.75), rgba(240, 238, 255, 0.55));
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.06);
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.nav-container .logo img {
  max-width: 80%;
  max-height: 80%;
  object-fit: contain;
}

/* 滚动后 logo 淡出隐藏 */
.nav-container .logo.logo-hide {
  opacity: 0;
  transform: translateX(-20px);
  pointer-events: none;
}

.nav-container .nav {
  display: flex;
  margin-left: 150px;
  align-items: center;
}




.nav-container .nav li {
  margin-top: 10px;
  margin-left: 50px;
  height: 52px;
}

.nav-container .nav li a {
  display: block;
  padding: 10px 20px;
  border-radius: 6px;
  transition: background-color 0.25s ease, color 0.25s ease;
}

.nav-container .nav li a:hover {
  background-color: rgba(255, 255, 255, 0.2);
  /* color: #fff; */
}

.nav-container.nav-glass .nav li a:hover {
  background-color: rgba(255, 255, 255, 0.35);
}
</style>
