<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import logo from "@/assets/img/welab.png"
import test2 from "@/assets/img/test2.png"
import test from "@/assets/img/test.png"
// 真实项目里这里应该是不同的图片路径
// 先拿同一张 logo 演示轮播逻辑，替换成真实图片就能看到效果
const photoList = ref([logo, test, test2])
const currentIndex = ref(0)
let timer = null

function stopCarousel() {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

function startCarousel() {
  stopCarousel()   // 先停旧的，确保只有一个
  timer = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % photoList.value.length
  }, 3000)
}

onMounted(startCarousel)
onUnmounted(stopCarousel)

const changeIndex = (index) => {
  currentIndex.value = index
  startCarousel()   // 立即重启，重置计时周期
}
const length = photoList.value.length
</script>
<template>
  <div class="main-card">
    <img :src="photoList[currentIndex]" alt="welab" />
    <ul>
      <li v-for="(item, index) in length" :key="index" :class="{ 'active': index === currentIndex }"
        @click="changeIndex(index)">
      </li>
    </ul>
  </div>

</template>
<style scoped>
.main-card {
  width: 600px;
  height: 400px;
  position: relative;
  border-radius: 24px;
  overflow: hidden;

  /* 磨砂玻璃 */
  background: linear-gradient(135deg,
      rgba(255, 255, 255, 0.55) 0%,
      rgba(255, 255, 255, 0.25) 40%,
      rgba(245, 240, 255, 0.35) 100%);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);

  /*  多层阴影：外投影 + 内高光 */
  box-shadow:
    0 24px 60px -12px rgba(0, 0, 0, 0.18),
    0 8px 24px -8px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.8),
    inset 0 -1px 0 rgba(255, 255, 255, 0.2);

  /*  细边框 + 顶部强高光 */
  border: 1px solid rgba(255, 255, 255, 0.35);
}

/* 顶部高光扫边 —— 像苹果设备的反光 */
.main-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 10%;
  background: linear-gradient(180deg,
      rgba(255, 255, 255, 0.25),
      transparent);
  pointer-events: none;
  z-index: 2;
}

.main-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  /* 图片叠一层半透明白，让毛玻璃能透出来 */
  /* filter: saturate(1.05); */
}

ul {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 14px;
  left: 50%;
  transform: translateX(-50%);
  list-style: none;
  z-index: 3;

  /* 指示器也套一层小玻璃胶囊 */
  padding: 6px 14px;
  border-radius: 20px;
  background: rgba(0, 0, 0, 0.18);
  backdrop-filter: blur(16px) saturate(140%);
  -webkit-backdrop-filter: blur(16px) saturate(140%);
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);

  li {
    margin: 0 5px;
    width: 8px;
    height: 8px;
    background-color: rgba(255, 255, 255, 0.4);
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.25s ease, width 0.25s ease, border-radius 0.25s ease;
    flex-shrink: 0;
  }

  li.active {
    background-color: #fff;
    width: 20px;
    height: 8px;
    border-radius: 4px;
    box-shadow: 0 0 8px rgba(255, 255, 255, 0.5);
  }
}
</style>
