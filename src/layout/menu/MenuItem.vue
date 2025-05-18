<template>
  <template v-for="menu in menuList" :key="menu.path">
    <!-- 无子路由 -->
    <template v-if="!menu.children">
      <el-menu-item
        :index="menu.path"
        v-if="!menu.meta?.hidden"
        style="padding-left: 20px; color: #ffffff"
      >
        <el-icon v-if="menu.meta?.icon">
          <component :is="menu.meta.icon"></component>
        </el-icon>
        <template #title>
          <span>{{ menu.meta?.title }}</span>
        </template>
      </el-menu-item>
    </template>

    <!-- 有一个子路由 -->
    <template v-if="menu.children && menu.children.length === 1">
      <el-menu-item
        :index="menu.path + '/' + menu.children[0].path"
        v-if="!menu.children[0].meta?.hidden"
        style="padding-left: 20px; color: #ffffff"
      >
        <el-icon v-if="menu.children[0].meta?.icon">
          <component :is="menu.children[0].meta.icon"></component>
        </el-icon>
        <template #title>
          <span>{{ menu.children[0].meta?.title }}</span>
        </template>
      </el-menu-item>
    </template>

    <!-- 有多个子路由，折叠 -->
    <el-sub-menu
      v-if="menu.children && menu.children.length > 1"
      :index="menu.path"
      style="padding-left: 0"
      popper-append-to-body
    >
      <template #title>
        <el-icon v-if="menu.meta?.icon">
          <component :is="menu.meta.icon"></component>
        </el-icon>
        <span>{{ menu.meta?.title }}</span>
      </template>
      <template v-for="child in menu.children" :key="child.path">
        <el-menu-item
          :index="menu.path + '/' + child.path"
          v-if="!child.meta?.hidden"
          style="padding-left: 40px"
        >
          <el-icon v-if="child.meta?.icon">
            <component :is="child.meta.icon"></component>
          </el-icon>
          <template #title>
            <span>{{ child.meta?.title }}</span>
          </template>
        </el-menu-item>
      </template>
    </el-sub-menu>
  </template>
</template>

<script lang="ts" setup>
import { defineProps } from "vue";

interface MenuItem {
  path: string;
  meta?: {
    title?: string;
    icon?: string;
    hidden?: boolean;
  };
  children?: MenuItem[];
  redirect?: string;
}

defineProps<{
  menuList: MenuItem[];
}>();
</script>

<style lang="scss" scoped>
.el-menu-item {
  background-color: #009c74 !important;
}

.el-menu-item.is-active {
  color: #00ffbf !important;
  background: #4bc0a1 !important;
}

.el-sub-menu__title {
  color: #34c9a3 !important;
  padding-left: 20px !important;
}

:deep(.el-sub-menu .el-menu) {
  .el-menu-item {
    padding-left: 40px !important;
  }
}

:deep(.el-menu--collapse) {
  .el-sub-menu__title {
    padding-left: 20px !important;
  }
}
.el-menu-item {
  margin: 4px 8px;
  border-radius: 8px;
  transition: all 0.3s ease;
}
.el-menu-item:hover {
  background-color: #4bc0a1 !important;
  border-radius: 8px !important;
  // transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: all 0.3s ease;
}


:deep(.el-menu--inline) {
  background-color: #009c74 !important;
}
</style>
