<script setup lang='ts'>

</script>

<template>
    <el-scrollbar>
        <el-menu>
            <el-sub-menu index="1">
                <template #title>Sub1</template>
                <el-menu-item-group title="Group1">
                    <el-menu-item index="1-1">Option 1</el-menu-item>
                    <el-menu-item index="1-2">Option 2</el-menu-item>
                </el-menu-item-group>
            </el-sub-menu>
            <el-sub-menu index="2">
                <template #title>Sub2</template>
                <el-menu-item-group title="Group2">
                    <el-menu-item index="2-1">Option 1</el-menu-item>
                    <el-menu-item index="2-2">Option 2</el-menu-item>
                </el-menu-item-group>
            </el-sub-menu>
        </el-menu>
    </el-scrollbar>
</template>

<style scoped></style>