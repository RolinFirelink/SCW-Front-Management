<template>
  <div class="item">
    <el-breadcrumb separator=" > ">
      <el-breadcrumb-item v-for="item in tabs">
        {{ item.meta.title }}
      </el-breadcrumb-item>
    </el-breadcrumb>
  </div>
  <div class="information">
    <div class="calendar">
      <el-icon class="icon"><Calendar /></el-icon>
      <SimpleCalendar />
    </div>
  </div>
  <div class="user">
    <img class="avater" :src="userInfo.userImage" alt="" />
    <div class="username">
      <span>{{ userInfo.username }}</span>
      <div>
        <el-dropdown class="userInfo" @command="handleCommand">
          <el-icon class="userIcon tool"><Tools /></el-icon>

          <template #dropdown>
            <el-dropdown-menu>
              <el-dropdown-item command="setting">个人设置</el-dropdown-item>
              <el-dropdown-item command="quit" divided
                >退出登录</el-dropdown-item
              >
            </el-dropdown-menu>
          </template>
        </el-dropdown>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, watch, onBeforeMount, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import { reqLogout } from "@/api/user/index";
import SimpleCalendar from "@/components/SimpleCalendar.vue";
import { ElMessage } from "element-plus";
import Cookies from "js-cookie";
// const { userInfo } = storeToRefs(user);
const userInfo = {
  username: "管理员",
  userImage:
    "https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png",
};

onMounted(() => {
  // user.getUserInfo();
});
// import { useStore } from "@/store/index";

// let count = ref();
// let hidden = ref(false);
// const store = useStore();
const tabs = ref([]);
const route = useRoute();
const router = useRouter();
const date = ref(new Date());

// const avater = computed(() => {
//   return store.state.avater || (sessionStorage.getItem("avater") as string)
// })

const getBreadCom = () => {
  let mached = route.matched.filter((item) => item.meta && item.meta.title);
  tabs.value = mached;
};
getBreadCom();
watch(
  () => route.path,
  () => getBreadCom()
);
//退出登录
const logout = async () => {
  const res = await reqLogout();
  if (res.code === "200") {
    ElMessage({
      type: "success",
      message: "退出登录成功",
    });
    Cookies.remove("auth_token");
    // Cookies.remove("user");
    router.push("/login");
  }
};
//人物图标路由跳转
const handleCommand = (command) => {
  switch (command) {
    case "quit":
      logout();
      break;
    case "setting":
      router.push("/setting/personal");
      break;
  }
};
</script>

<style lang="scss" scoped>
.item {
  width: 25%;
  background-color: #fff;
  height: 50px;
  display: flex;
  justify-content: center;
  border-radius: 20px;
  .el-breadcrumb {
    font-size: 15px !important;
    line-height: 50px;
  }
}
.information {
  width: 35%;
  background-color: #fff;
  height: 50px;
  display: flex;
  justify-content: flex-start;
  border-radius: 20px;
  .calendar {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 0 20px;
  }
  .icon {
    display: inline;
    line-height: 50px;
    margin-right: 10px;
    font-size: 30px;
    cursor: pointer;
  }
}
.user {
  width: 20%;
  background-color: #fff;
  height: 50px;
  border-radius: 20px;
  display: flex;
  .avater {
    border-radius: 50%;
    width: 50px;
    height: 50px;
  }
  .username {
    display: flex;
    width: 70%;
    font-size: 16px;
    margin-left: 10px;
    justify-content: space-between;
    align-items: center;
    min-width: 110px;
    .userIcon {
      margin-top: 5px;
      font-size: 25px;
    }
    .tool {
      margin-left: 5px;
    }
  }

  .userInfo {
    cursor: pointer;
    margin-left: 20px;
  }
}
:deep(.el-breadcrumb__inner) {
  color: #a8abb2 !important;
  font-weight: 700 !important;
}
</style>
