<script setup lang="ts">
import { RouterView } from 'vue-router';
import TheAside from './components/TheAside.vue';
import TheFooter from './components/TheFooter.vue';
import TheHeader from './components/TheHeader.vue';
</script>

<template>
  <el-container class="main-container">
    <el-header>
      <TheHeader />
    </el-header>
    <el-container class="main-content">
      <el-aside>
        <TheAside />
      </el-aside>
      <el-main>
        <RouterView />
      </el-main>
    </el-container>
    <el-footer>
      <TheFooter />
    </el-footer>
  </el-container>
</template>

<style scoped>
.main-container {
  padding-left: 2vw;
  padding-right: 2vw;

  padding-top: 2vh;
  padding-bottom: 2vh;
}

.el-header {
  background-color: #B3C0D1;
  color: #333;
  text-align: center;
  line-height: 60px;
}

.main-content .el-aside {
  background-color: var(--el-color-primary-light-7);
  color: var(--el-text-color-primary);
  text-align: center;
  line-height: 60px;

  min-height: 80vh;
}

.el-footer {
  background-color: #903148;
  color: #333;
  text-align: center;
  line-height: 60px;
}
</style>
