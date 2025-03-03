<script setup lang='ts'>
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';

// 书籍信息
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

// 分页信息
interface PaginationInfo {
    totalItem: number;
    totalPage: number;
    currentPage: number;
    pageSize: number;
}

const paginationInfo = ref<PaginationInfo>(
    {
        totalItem: 0,
        totalPage: 0,
        currentPage: 1,
        // 分页大小默认为10 
        // 后端限制 分页大小最高为20
        pageSize: 10,
    }
)


const getEbookList = async (paginationInfo: PaginationInfo) => {
    // const res = await axios.get(`http://localhost:8080/ebook/select?pageNum=${pageNum}&pageSize=${pageSize}`);
    const res = await axios.get("http://localhost:8080/ebook/select", {
        params: {
            pageNum: paginationInfo.currentPage,
            pageSize: paginationInfo.pageSize
        }
    });

    // 获取书籍列表
    bookList.value = res.data.content.list;

    // 获取总条目数以及分页总数
    paginationInfo.totalItem = res.data.content.totalItem;
    paginationInfo.totalPage = res.data.content.totalPage;
}


// 加载时 获取书籍列表
onMounted(() => getEbookList(paginationInfo.value));

// 监听 currentPage 和 pageSize 的变化
watch([() => paginationInfo.value.currentPage, () => paginationInfo.value.pageSize], () => {
    getEbookList(paginationInfo.value);
});

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
        <el-pagination v-model:current-page="paginationInfo.currentPage" v-bind:page-count="paginationInfo.totalPage"
            v-on:current-change="getEbookList(paginationInfo)" background layout="prev, pager, next" />
    </div>

</template>

<style scoped></style>