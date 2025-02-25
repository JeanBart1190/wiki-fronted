<script setup lang='ts'>
import axios from 'axios';

function getBook(): void {
    axios.get('http://localhost:8080/ebook/select?bookname=教程').then((res) => {
        console.log(res.data.content);
        // bookDao.value = res.data.content;
        // console.log(bookDao.value);
    });
}
</script>


<!-- 顶栏组件 -->
<template>
    <el-menu mode="horizontal">
        <el-menu-item>
            首页
        </el-menu-item>
        <el-menu-item>
            电子书管理
        </el-menu-item>
        <el-menu-item>
            关于我们
        </el-menu-item>
    </el-menu>
</template>

<style scoped>
.el-menu {
    width: 100%;
    /* background-color: rgb(201, 51, 204); */
}

.el-menu--horizontal {
    --el-menu-horizontal-height: 100%;
}
</style>