<template>
    <div class="navgation">
      <div class="content">
        <span>江南中街道党群服务中心</span>
      </div>
    </div>
</template>

<script>
    export default {
        name: "navigation"
    }
</script>

<style scoped lang="less">
  .navgation{
    width: 100%;
    height: 150rpx;
    background: #fff;
    position: fixed;
    z-index:999;
    top:0;
    left: 0;
    .content{
      width: 692rpx;
      height: 150rpx;
      background: #fff;
      padding-top:56rpx;
      margin:0 auto;
      box-sizing: border-box;
      span{
        font:36rpx "黑体";
        padding-top:18rpx;
      }
    }
  }
</style>
