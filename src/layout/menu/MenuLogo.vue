<template>
  <div class="logo">
    <img :src="logo" alt="logo" />
    <span v-if="!isCollapse" class="title">智慧柑橘管理平台</span>
  </div>
</template>
<script setup lang="ts">
import { computed } from "vue";
import { useStore } from "@/store/index";
import logo from "@/assets/logo.png";
const store = useStore();
const isCollapse = computed(() => {
  return store.getters["getCollapse"];
});
</script>
<style lang="scss" scoped>
.logo {
  background-color: #009c74;
  height: 55px;
  border-bottom: 2px solid #fff;
  line-height: 50px;
  display: flex;
  align-items: center;
  padding-left: 15px;
  color: white;

  img {
    width: 40px;
    height: 40px;
    margin-right: 7px;
    border-radius: 50%;
  }

  span {
    font-weight: 600;
    line-height: 53px;
    font-size: 18px;
    vertical-align: middle;
  }
}
</style>
