<template>
  <el-container class="container">
    <el-aside class="asside" width="auto">
      <MenuBar></MenuBar>
    </el-aside>
    <el-container class="back">
      <el-header class="header">
        <Header></Header>
      </el-header>
      <el-main class="main">
        <div class="body">
          <router-view></router-view>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>
<script setup lang="ts">
import Header from "@/layout/header/Header.vue";
import MenuBar from "@/layout/menu/MenuBar.vue";
</script>
<style lang="scss" scoped>
.back {
  background-image: linear-gradient(
    rgba(222, 255, 238, 0.279),
    rgba(222, 255, 238, 0.3)
  );
  background-repeat: repeat;
  min-width: 1000px;
  min-height: 665px;
}
.container {
  height: 100vh;
}

.asside {
  background-color: #009c74;
  min-height: 665px;
  padding: 10px;
  border-radius: 16px;
  box-shadow: 4px 0 12px rgba(0, 0, 0, 0.1);
}

.header {
  padding-top: 1vh;
  height: 7vh;
  min-height: 65px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  background-color: transparent;
  min-width: 1000px;
}
.main {
  margin: 0;
  padding: 0;
  padding-top: 1vh;
  // background-color: transparent;
  min-width: 1000px;
  min-height: 600px;
  height: 91vh;
  .body {
    width: 94%;
    margin: 2% 3%;
    height: 92%;
    // background-color: #ffffff;
    border-radius: 10px;
  }
}
</style>
