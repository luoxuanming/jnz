<template>
  <div class="wybs">
    <div class="imggroup">
      <img src="../../images/wybs.png" alt="" class="wybs_bg">
      <img src="../../images/dangwu.png" alt="" class="wimg" @click="goDwzn">
      <img src="../../images/zhengwu.png" alt="" class="wimg" @click="goZw">
    </div>
    <div class="logo_container">
      <img src="../../images/logo.png" alt="" class="logo">
    </div>
  </div>
</template>

<script>

  import * as conf from '../../utils/config'
  export default {
    components: {

    },

    data () {
      return {
        show:true
      }
    },
    methods:{
      goDwzn(){
        wx.navigateTo({
          url:`/pages/dwzn/main`
        });
      },
      goZw(){
        wx.navigateTo({
          url:`/pages/outLink/main?type=3`
        });
      }
    },
    onLoad() {

    }
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  @import "../../common/css/font/iconfont.css";
  .wybs{
    width: 100%;
    height: 100vh;
    position: fixed;
    bottom: 0;
    overflow: hidden;
    .wybs_bg{
      width: 100%;
      height: 323rpx;
      margin-bottom:36rpx;
      position: fixed;
      top: 0;
      left: 0;
    }
    .imggroup{
      width: 100%;
      height: 100vh;
      padding-top:358rpx;
      overflow: hidden;
      box-sizing: border-box;
      text-align: center;
      position: absolute;
      top:0;
      left: 0;
      .wimg{
        width: 690rpx;
        height:344rpx;
        margin: 0 auto;
        margin-bottom:28rpx;
      }
    }
    .logo_container{
      position: absolute;
      width: 100%;
      bottom: 30rpx;
      display: flex;
      justify-content: center;
      .logo{
        width: 363rpx;
        height: 70rpx;
        margin:0 auto;
      }
    }
  }
</style>
