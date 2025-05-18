<template>
    <div class="change">
        <el-icon class="icons" @click="changeIcon">
            <component :is="status ? 'Expand' : 'Fold'"></component>
        </el-icon>
    </div>
</template>
<script lang='ts' setup>
import { ref } from 'vue';
import { useStore } from '@/store/index';
const store = useStore()
const status = ref(false)
const changeIcon = ()=>{
    status.value = !status.value
    store.commit('setCollapse',status.value)
}
</script>
<style scoped lang="scss">
.icons {
    width: 100%;
    display: flex;
    align-items: center;
    font-size: 25px;
    color: #303133;
    cursor: pointer;
    margin-right: 15px;
}
.change {
    width: 45px;
    height: 45px;
    margin-right: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: #fff;
    border-radius: 50%;
}
</style>