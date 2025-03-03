<script setup lang='ts'>
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

// pageSize暂时用不到
const bookList = ref<BookInfo[]>([]);
const currentPage = ref(1);
// 分页大小 初步设置为一页十条
const pageSize = ref(10);

const getEbookList = async (pageNum: Number, pageSize: Number) => {
    const res = await axios.get(`http://localhost:8080/ebook/select?pageNum=${pageNum}&pageSize=${pageSize}`);

    bookList.value = res.data.content.list;
}

// 加载时 获取书籍列表
onMounted(() => getEbookList(currentPage.value, pageSize.value));

</script>

<template>
    <el-table :data="bookList" style="width: 100%; margin-bottom: 20vh;">
        <el-table-column prop="id" label="Id" />
        <el-table-column prop="name" label="Name" />
        <el-table-column prop="doc_count" label="Doc_count" />
        <el-table-column prop="view_count" label="View_count" />
        <el-table-column prop="Vote" label="Vote_count" />
        <el-table-column fixed="right" label="Operations" min-width="120">
            <template #default>
                <el-button link type="primary" size="small">
                    Detail
                </el-button>
                <el-button link type="primary" size="small">
                    Edit
                </el-button>
            </template>
        </el-table-column>
    </el-table>
    <div style="display: flex; justify-content: flex-end;">

        <!-- 分页组件 双向绑定currentPage; currentPage 改变时 触发获取书籍列表事件-->
        <el-pagination v-model:current-page="currentPage" v-on:current-change="getEbookList(currentPage, pageSize)"
            background layout="prev, pager, next" :total="1000" />
    </div>

</template>

<style scoped></style>