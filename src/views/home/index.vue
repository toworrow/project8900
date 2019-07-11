<template>
<el-container class="home-container">
    <el-aside class="my-aside" width="200px">Aside</el-aside>
    <el-container>
      <el-header class="my-header">Header</el-header>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>
<script>
export default {

}
</script>
<style lang="less">
.home-container{
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  .my-aside{
    background: #002033;
  }
  .my-header{
    border-bottom: 1px solid #ddd;
  }
}
</style>
