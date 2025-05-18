<template>
  <MenuLogo></MenuLogo>
  <el-menu
    :default-active="activeMenu"
    :unique-opened="true"
    class="el-menu-vertical-demo"
    :collapse="isCollapse"
    router
    @select="handleMenuSelect"
  >
    <MenuItem :menuList="menuList"> </MenuItem>
  </el-menu>
</template>
<script lang="ts" setup>
import { reactive, computed, onMounted } from "vue";
import { useStore } from "@/store/index";
import MenuItem from "@/layout/menu/MenuItem.vue";
import MenuLogo from "@/layout/menu/MenuLogo.vue";
import { useRouter, useRoute } from "vue-router";
import { constantRoute } from "@/router/router";

const router = useRouter();
const route = useRoute();

const menuList = constantRoute.filter((route) => {
  // 过滤掉登录、注册页面
  if (route.meta?.hidden === true) {
    return false;
  }

  // 如果是根路由，显示其子路由
  if (route.path === "/") {
    return route.children && route.children.length > 0;
  }

  return true;
});
// console.log("生成的menuList", menuList);

const store = useStore();
const isCollapse = computed(() => {
  return store.getters["getCollapse"];
});

// 获取当前激活的菜单项
const activeMenu = computed(() => {
  const { path, matched } = route;
  return path;
});

// 处理菜单点击
const handleMenuSelect = (index: string) => {
  if (route.path !== index) {
    // 如果是操作管理，直接跳转到grow页面
    router.push(index);
  }
};
</script>
<style lang="scss" scoped>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  // width: 180px;
  min-height: 400px;
  background-color: #009c74;
}

.el-menu {
  border-right: none;
  background-color: #009c74;
}

:deep(.el-sub-menu .el-sub-menu__title) {
  color: #ffffff !important;
}

:deep(.el-sub-menu__title) {
  background-color: #009c74 !important;
}

:deep(.el-menu .el-menu-item) {
  color: #bfd9ce;
  &:nth-last-child(1) {
    border-bottom: 0.1px solid rgba(248, 248, 248, 0.208);
  }
}
:deep(.el-menu-item.is-active) {
  color: #00ffbf !important;
  text-shadow: 1px 1px #00684e;
}

:deep(.is-opened .el-menu-item) {
  background-color: #009c74 !important;
}

:deep(.el-menu-item:hover) {
  background-color: #4bc0a1 !important;
}
</style>
