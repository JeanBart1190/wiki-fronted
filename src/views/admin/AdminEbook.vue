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

const bookList = ref<BookInfo[]>([]);

const getEbookList = async () => {
    const res = await axios.get('http://localhost:8080/ebook/select?bookname=');
    // console.log(res.data.content);
    bookList.value = res.data.content;
}

onMounted(() => getEbookList());

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
        <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>

</template>

<style scoped></style>