<script setup lang="ts">
import TheAside from '@/components/TheAside.vue';
import axios from 'axios';
import { onMounted, ref } from 'vue';

interface BookInfo {
  id: number;
  name: string;
  category1_id: number;
  categpru2_id: number;
  description: string;
  cover: string;
  doc_count: number;
  view_count: number;
  vote_count: number;
}

const bookList = ref<BookInfo[]>([]);

const getEbookList = async () => {
  const res = await axios.get('http://localhost:8080/ebook/select?bookname=');
  // console.log(res.data.content);
  bookList.value = res.data.content;
}

onMounted(() => {
  getEbookList();
});
</script>

<template>
  <el-container>
    <!-- 侧边栏 -->
    <el-aside>
      <TheAside />
    </el-aside>

    <!-- 侧边栏对应内容 -->
    <el-main>
      <el-row :gutter="20">
        <el-col :span="8" v-for="(book, index) in bookList" :key="index">

          <el-card>
            <!-- 自定义卡片头 -->
            <template #header>
              <div>
                {{ book.name }}
              </div>
            </template>
            <!-- 卡片内容 -->
            <div style="padding: 5%;">{{ book.description }}</div>
          </el-card>

        </el-col>
      </el-row>
    </el-main>
  </el-container>
</template>

<style scoped>
.block {
  display: block;
  width: 100%;
  height: 100%;
  background-color: red;
}

.el-aside {
  background-color: var(--el-color-primary-light-7);
  color: var(--el-text-color-primary);
  text-align: center;
  line-height: 60px;

  min-height: 75vh;
}

.el-row {
  margin-top: 10px;
  margin-bottom: 20px;
}

.el-card {
  margin-bottom: 20px;
}
</style>
