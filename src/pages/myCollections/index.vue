<template>
  <div class="myCollections">
    <div class="coll_container">
      <div class="zl_list" v-if="list.length" v-for="(item,index) in list" :key="index" @click="goTwzlRes(item.DOC_ID)">
        <img :src="item.DOC_IMG" @error="errorfn(index)" class="zl_img" alt="">
        <dl>
          <dt>{{item.DOC_NAME}}</dt>
          <dd>
            <div>总课程<span>{{item.RES_COUNT}}</span>节</div>
            <!--<div>{{item.CREATE_TIME}}</div>-->
            <div class="count">{{item.DOC_SCORE}}学分</div>
          </dd>
        </dl>
      </div>
      <div class="kong" v-if="!list.length">
        <img src="../../images/ly_null0.png" alt="">
        <div class="msg">暂无收藏资料</div>
      </div>
    </div>
  </div>
</template>

<script>
  import * as conf from "../../utils/config"
  export default {

    data () {
      return {
        list:[1,1]
      }
    },
    methods:{
      getfavList(){
        //获取收藏图文资料收藏列表
        var that=this;
        wx.getStorage({
          key: 'userInfos',
          success(ret) {
            //console.log(ret.data.USER_ID);
            wx.request({
              url:`${conf.HOST}/stddj-gzgj/servlet/twzl.action?method=getfavList`,
              data:{
                userId:ret.data.USER_ID
              },
              success(res){
                //console.log(JSON.stringify(res.data))
                that.list=res.data;
              }
            })
          }
        })
      },
      goTwzlRes(id){
        //console.log(id)
        wx.getStorage({
          key: 'userInfos',
          success(res) {
            wx.navigateTo({
              url:`/pages/twzljj/main?docId=${id}&userId=${res.data.USER_ID}`
            })
          },
          fail(){
            wx.showToast({
              title:"请登录后重试",
              icon:"none",
              duration:2000,
              success(){

              }
            })
            setTimeout(function(){
              wx.navigateTo({
                url:`/pages/login/main`
              })
            },2000)
          }
        })
      },
      errorfn(index){
        this.list[index].NEWS_THUMB_IMG="../../images/default_img.jpg"
      }
    },
    onShow() {
      this.getfavList();
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  .myCollections{
    width: 100%;
    .coll_container{
      width: 100%;
      padding:0 30rpx;
      box-sizing: border-box;
    }
    .kong{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      .msg{
        width: 100%;
        font:30rpx "微软雅黑";
        text-align: center;
        position: absolute;
        left: 0;
        top:700rpx;
        color:#c4caee;
      }
    }
    .zl_list{
      width: 100%;
      height:160rpx;
      background: #fff;
      padding:0 18rpx;
      box-sizing: border-box;
      /*box-shadow: 0 0 6rpx rgba(243,243,243,.6);*/
      border-bottom: 1rpx solid rgba(243,243,243,1);
      border-radius: 10rpx;
      display:flex;
      align-items: center;
      overflow: hidden;
      margin-bottom: 20rpx;
      .zl_img{
        width: 172rpx;
        height: 112rpx;
        border-radius:10rpx;
        float: left;
      }
      dl{
        flex: 1;
        overflow: hidden;
        padding-left: 26rpx;
        box-sizing: border-box;
        dt{
          font:30rpx "微软雅黑";
          color:#333333;
          white-space: nowrap;
          padding-right: 30rpx;
          box-sizing: border-box;
          overflow: hidden;
          text-overflow: ellipsis;
          margin-bottom: 20rpx;
        }
        dd{
          font:22rpx "黑体";
          color:#7f8699;
          display: flex;
          justify-content: space-between;
          span{
            color:#333;
          }
          .count{
            color:@mainColor;
          }
        }
      }
    }
  }
</style>
