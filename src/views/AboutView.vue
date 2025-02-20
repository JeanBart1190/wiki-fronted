<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>

<style>
/* 只有当视口宽度大于等于 1024 像素时，内部的样式才会生效 */
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
