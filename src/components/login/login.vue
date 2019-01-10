<template>
    <div class="login">
      <img src="../../images/login.png" alt="" class="login_bg">
      <div class="user_info">
        <img :src="userInfos.avatarUrl" :alt="userInfos.avatarUrl">
        <span class="username">{{userInfos.nickName}}</span>
        <span>积分：30</span>
        <button v-if="canIUse" open-type="getUserInfo" @click="goLogin" :plain="true" lang="zh_CN" bindgetuserinfo="onGotUserInfo">请登录</button>
      </div>
      <div class="temperature">
        <img src="../../images/cloud.png" alt="">
        <span>20℃</span>
      </div>
    </div>
</template>

<script>
  import {mapState,mapMutations,mapGetters} from "Vuex";
    export default {
        data(){
          return{
            getuserinfo:{},
          }
        },
        computed:{
          ...mapGetters({
            userInfos:"userInfos",
            token:"token"
          })
        },
        created:function(){
          // console.log(JSON.stringify(this.token));
        },
        methods:{
          goLogin(){
            wx.navigateTo({
              url:`/pages/login/main`
            });
          },
          onGotUserInfo: function(e) {
            console.log(e.detail.errMsg)
            console.log(e.detail.userInfo)
            console.log(e.detail.rawData)
          }
        },
        onLoad(){

      },
        watch:{

        }
    }
</script>

<style scoped lang="less">

  .login{
    width:692rpx;
    height:252rpx;
    background: #fff;
    margin:0 auto;
    position:relative;
    .login_bg{
      width:100%;
      height:252rpx;
      display:flex;
      position: relative;
      z-index: 10;
    }
    .user_info{
      position: absolute;
      width:692rpx;
      height:90rpx;
      bottom:0;
      left:0;
      display:flex;
      align-items:center;
      box-sizing:border-box;
      padding:0 26rpx;
      z-index: 10;
      img{
        width:68rpx;
        height:68rpx;
        border-radius:34rpx;
        box-shadow:2rpx 2rpx 3rpx rgba(221,221,221,0.7);
        position: relative;
        margin-top:-8rpx;
      }
      .username{
        font:32rpx "黑体";
        margin-left:16rpx;
      }
      span:nth-of-type(2),button{
        font:28rpx "黑体";
        margin-left:22rpx;
        color:#7f8699;
      }
      button{
        position:absolute;
        right:26rpx;
        border:none
      }
    }
    .temperature{
      position: absolute;
      width:100%;
      height:22rpx;
      top:30rpx;
      left:0;
      padding-left:66rpx;
      z-index: 20;
      img{
        width:44rpx;
        height:32rpx;
        position:absolute;
        left:10rpx;
        top:0rpx;
        animation:cloud 2s linear infinite alternate;
      }
      span{
        font:24rpx "微软雅黑";
        color:#999999;
        position:absolute;
        left:65rpx;
        top:0rpx;
      }
    }
  }
  //温度云运动
  @keyframes cloud {
    0%{}
    100%{
      transform: translateX(10rpx);
    }
  }
</style>
