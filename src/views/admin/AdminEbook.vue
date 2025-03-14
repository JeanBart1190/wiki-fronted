<script setup lang="ts">
import axios from 'axios'
import { onMounted, ref } from 'vue'


// 书籍信息
interface BookInfo {
    id: number
    name: string
    category1_id: number
    categpry2_id: number
    description: string
    cover: string
    doc_count: number
    view_count: number
    vote_count: number
}
const bookList = ref<BookInfo[]>([])

// 当前编辑的书籍
const currentEditBook = ref<BookInfo>({
    id: 0,
    name: '',
    category1_id: 0,
    categpry2_id: 0,
    description: '',
    cover: '',
    doc_count: 0,
    view_count: 0,
    vote_count: 0
})


// 分页信息
interface PaginationInfo {
    totalItem: number
    totalPage: number
    currentPage: number
    pageSize: number
}

const paginationInfo = ref<PaginationInfo>({
    totalItem: 0,
    totalPage: 0,
    currentPage: 1,
    // 分页大小默认为10
    // 后端限制 分页大小最高为20
    pageSize: 2,
})



// 对话框可见性
const dialogVisible = ref(false)

// 分页获取电子书列表
const getEbookList = async (paginationInfo: PaginationInfo) => {
    // const res = await axios.get(`http://localhost:8080/ebook/select?pageNum=${pageNum}&pageSize=${pageSize}`);
    const res = await axios.get('http://localhost:8080/ebook/select', {
        params: {
            pageNum: paginationInfo.currentPage,
            pageSize: paginationInfo.pageSize,
        },
    })

    // 获取电子书列表
    bookList.value = res.data.content.list

    // 获取总条目数以及分页总数
    paginationInfo.totalItem = res.data.content.totalItem
    paginationInfo.totalPage = res.data.content.totalPage
}

// 编辑按钮点击事件
const handleEdit = async (book: BookInfo) => {
    // 获取当前行的书籍信息
    currentEditBook.value = { ...book };

    // 对话框可见
    dialogVisible.value = true;
}

// 表单保存
const saveEbook = async () => {
    console.log(currentEditBook.value)

    const res = await axios.post('http://localhost:8080/ebook/edit', {
        id: currentEditBook.value.id,
        name: currentEditBook.value.name,
        category1Id: currentEditBook.value.category1_id,
        category2Id: currentEditBook.value.categpry2_id,
        description: currentEditBook.value.description,
        cover: currentEditBook.value.cover,
        docCount: currentEditBook.value.doc_count,
        viewCount: currentEditBook.value.view_count,
        voteCount: currentEditBook.value.vote_count,
    })

    console.log('相应状态:' + res.data.message)
    if (res.data.success == true) {
        getEbookList(paginationInfo.value)
    }
}

// 加载时 获取书籍列表
onMounted(() => getEbookList(paginationInfo.value))

// 
</script>

<template>
    <el-table :data="bookList" style="width: 100%; margin-bottom: 20vh">
        <el-table-column prop="id" label="Id" />
        <el-table-column prop="name" label="Name" />
        <el-table-column prop="doc_count" label="Doc_count" />
        <el-table-column prop="view_count" label="View_count" />
        <el-table-column prop="Vote" label="Vote_count" />
        <el-table-column fixed="right" label="Operations" min-width="120">
            <template #default="{ row }">
                <el-button link type="primary" size="small"> Detail </el-button>
                <el-button link type="primary" size="small" v-on:click="handleEdit(row)">
                    Edit
                </el-button>
            </template>
        </el-table-column>
    </el-table>

    <el-dialog v-model:model-value="dialogVisible" title="Edit" style="width: 25vw">
        <el-form label-width="auto">
            <el-form-item label="封面">
                <el-input v-model="currentEditBook.cover" />
            </el-form-item>
            <el-form-item label="名称">
                <el-input v-model="currentEditBook.name" />
            </el-form-item>
            <el-form-item label="分类一">
                <el-input :value="currentEditBook.category1_id" />
            </el-form-item>
            <el-form-item label="分类二">
                <el-input :value="currentEditBook.categpry2_id" />
            </el-form-item>
            <el-form-item label="描述">
                <el-input :value="currentEditBook.description" />
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="saveEbook">Create</el-button>
                <el-button>Cancel</el-button>
            </el-form-item>
        </el-form>
    </el-dialog>

    <div style="display: flex; justify-content: flex-end">
        <!-- 分页组件 双向绑定currentPage; currentPage 改变时 触发获取书籍列表事件-->
        <el-pagination v-model:current-page="paginationInfo.currentPage" v-bind:page-count="paginationInfo.totalPage"
            v-on:current-change="getEbookList(paginationInfo)" background layout="prev, pager, next" />
    </div>
</template>

<style scoped></style>
