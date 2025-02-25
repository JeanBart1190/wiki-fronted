<script setup lang="ts">
import { RouterView } from 'vue-router';
import TheFooter from './components/TheFooter.vue';
import TheHeader from './components/TheHeader.vue';
</script>

<template>
  <el-container class="main-container">

    <!-- 顶栏 -->
    <el-header>
      <TheHeader />
    </el-header>

    <el-main>
      <!-- 主要内容 通过顶栏切换 -->
      <router-view />
    </el-main>

    <!-- 底栏/页脚 -->
    <el-footer>
      <TheFooter />
    </el-footer>

  </el-container>
</template>

<style scoped>
.el-header {
  /* background-color: rgb(51.2, 126.4, 204); */
  /* background-color: #B3C0D1; */
  color: #333;
  text-align: center;
  line-height: 60px;
}

.el-footer {
  background-color: #903148;
  color: #333;
  text-align: center;
  line-height: 60px;
}
</style>
