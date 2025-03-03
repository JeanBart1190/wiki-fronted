<script lang="ts" setup>

import { ref } from 'vue';

const colorList: string[] = [
    'red',
    'yellow',
    'blue'
]
const currentItem = ref<number>(0);
const currentColor = ref<string>(colorList[0]);

const testVBind = ref(1);

const changeColor = () => {
    currentItem.value = (currentItem.value + 1) % colorList.length;
    currentColor.value = colorList[currentItem.value];
}

const tableData = [
    {
        date: '2016-05-03',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
    },
    {
        date: '2016-05-02',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
    },
    {
        date: '2016-05-04',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
    },
    {
        date: '2016-05-01',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
    },
]
</script>

<template>
    <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="Date" width="180" />
        <el-table-column prop="name" label="Name" width="180" />
        <el-table-column prop="address" label="Address" />
    </el-table>

    <!-- 测试CSS绑定 -->
    <div style="width: 100%; height: 20vh; background-color: darkgray;">
        <button :style="{ backgroundColor: currentColor }" v-on:click="changeColor"> test </button>
        <button style="background-color: darkgreen;">test2</button>
        <div style="width: 100%; height: 20vh; font-size: larger;">
            {{ testVBind }}
        </div>
    </div>

    <el-pagination v-model:current-page="testVBind" background layout="prev, pager, next" :total="1000" />
</template>



<style scoped></style>