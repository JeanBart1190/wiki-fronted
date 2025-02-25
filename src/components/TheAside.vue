<script setup lang='ts'>

import { onMounted, ref } from 'vue';
import type { RouteRecordRaw } from 'vue-router';
import { useRouter } from 'vue-router';

const router = useRouter();
const routes = ref<RouteRecordRaw[]>([]);

function testRouter(): void {
    routes.value = [...router.options.routes];
    routes.value.forEach((item) => {
        console.log(item.path);
    })
    console.log(router.options.routes);
}

onMounted(() => {
    testRouter();
});
</script>

<!-- 侧边栏组件 -->
<template>
    <el-scrollbar>
        <el-menu router: true>
            <el-menu-item v-for="(item, index) in routes" :index="index.toString()" :route="item.path">
                {{ item.name }}
            </el-menu-item>
        </el-menu>
    </el-scrollbar>
</template>

<style scoped></style>