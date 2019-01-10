<template>
  <div class="gjgz">
    <img src="../../images/gjgz.png" alt="" class="gjgz_bg">
    <div class="content">
      <div class="box">
        <img src="../../images/gjgz01.png" mode="widthFix" alt="">
        <div class="layer" @click="goZddw">
          <div>
            <span class="iconfont1 icon-zhongdiandanwei1"></span>
          </div>
          <dl>
            <dt>重点单位</dt>
            <dd>江南中地区党建联合会，构建社会治理新格局</dd>
          </dl>
        </div>
      </div>
      <div class="box">
        <img src="../../images/gjgz02.png" mode="widthFix" alt="">
        <div class="layer" @click="goLdbywy">
          <div>
            <span class="iconfont1 icon-liangdaibiaoyiweiyuan1"></span>
          </div>
          <dl>
            <dt>两代表一委员</dt>
            <dd>搭建干部群众的“连心桥</dd>
          </dl>
        </div>
      </div>
      <div class="box">
        <img src="../../images/gjgz03.png" mode="widthFix" alt="">
        <div class="layer" @click="goWyly">
          <div>
            <span class="iconfont1 icon-woyaoliuyan1"></span>
          </div>
          <dl>
            <dt>我要留言</dt>
            <dd>广开言路，网汇民声，传递民意，政通人和</dd>
          </dl>
        </div>
      </div>
    </div>
    <div class="logo_container">
      <img src="../../images/logo.png" alt="" class="logo">
    </div>
  </div>
</template>

<script>


export default {
  components: {

  },

  data () {
    return {

    }
  },
  methods:{
    goZddw(){
      wx.navigateTo({
        url:`/pages/zddw/main`
      });
    },
    goWyly(){
      wx.getStorage({
        key: 'userInfos',
        success(res) {
          // console.log(JSON.stringify(res.data.USER_ID))
          wx.navigateTo({
            url:`/pages/wyly/main?userId=${res.data.USER_ID}`
          });
        },
        fail(){
          wx.showToast({
            title:"请登录后重试",
            icon:"none",
            duration:2000
          })
          setTimeout(function(){
            wx.navigateTo({
              url:`/pages/index/main`
            })
          },2000)
        }
      })

    },
    goLdbywy(){

      wx.navigateTo({
        url:`/pages/ldbywy/main`
      });
    }
  },
  created () {

  }
}
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
.gjgz{
  width: 100%;
  height: 100vh;
  position: fixed;
  bottom: 0;
  overflow: hidden;
  background: url("../../images/logo.png") no-repeat;
  background-size: 363rpx 70rpx;
  background-position: center bottom 30rpx;
  .gjgz_bg{
    width: 100%;
    height: 364rpx;
  }
  .content{
    position: relative;
    left:0;
    top:0;
    width: 690rpx;
    height: 100vh;
    margin: 0 auto;
    .box{
      position: relative;
      width: 100%;
      height: 200rpx;
      margin-bottom: 30rpx;
      img{
        width: 100%;
        margin-bottom: 25rpx;
      }
      .layer{
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top:0;
        z-index: 99;
        display: flex;
        align-items: center;
        div{
          width: 96rpx;
          height: 96rpx;
          -webkit-border-radius: 50%;
          -moz-border-radius: 50%;
          border-radius: 50%;
          background: #fff;
          display: flex;
          align-items: center;
          justify-content: center;
          margin-left: 28rpx;
          margin-right: 28rpx;
          span{
            width: 54rpx;
            height: 54rpx;
          }
        }
        dl{
          color:#333;
          dt{
            font:600 40rpx "黑体";
            margin-bottom: 18rpx;
          }
          dd{
            font:26rpx "黑体";
            color:#7f8699;
          }
        }
      }
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
