<!-- 时间显示组件 -->
<template>
  <div class="time">
    <span>{{ formattedTime }}</span>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from "vue";

const now = ref(new Date());

const formattedTime = computed(() => {
  const date = now.value;
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const day = String(date.getDate()).padStart(2, "0");
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");
  const week = date.getDay();
  const weekArr = [
    "星期日",
    "星期一",
    "星期二",
    "星期三",
    "星期四",
    "星期五",
    "星期六",
  ];

  return `${year}年${month}月${day}日 ${hours}:${minutes}:${seconds} ${weekArr[week]}`;
});

let timer = null;

onMounted(() => {
  timer = setInterval(() => {
    now.value = new Date();
  }, 1000);
});

onUnmounted(() => {
  if (timer) {
    clearInterval(timer);
  }
});
</script>

<style scoped>
.time {
  margin-left: 65px;
  font-size: 15px;
  color: #000000;
  width: 240px;
}
</style>
