<template>
  <div class="wyly">
    <scroll-view class="scroll" v-if="list.length" :scroll-y="true">
      <div  class="lyb">
        <div class="list" v-for="(item,index) in list" :key="index">
          <div class="info">
            <div class="title">
              {{item.COMMENT_TITLE}}
            </div>
            <div class="time">{{item.CREATE_TIME}}</div>
          </div>
          <div class="state">
            <div class="btn" :class="item.COMMENT_STATUS=='已回复'?'ok':''">{{item.COMMENT_STATUS}}</div>
          </div>
        </div>
        <!--<div class="list">-->
          <!--<div class="info">-->
            <!--<div class="title">-->
              <!--随着国家改革开放和经济的迅猛发展作为民族振兴基石的教育事业教育事业教育事业-->
            <!--</div>-->
            <!--<div class="time">2018-12-15 10:06</div>-->
          <!--</div>-->
          <!--<div class="state">-->
            <!--<div class="btn ok">已回复</div>-->
          <!--</div>-->
        <!--</div>-->
      </div>
    </scroll-view>
    <div v-if="!list.length" class="null">
      <img src="../../images/ly_null.png" mode="widthFix" alt="">
      <div class="ly_btn" @click="golyform">我要留言</div>
    </div>
    <div v-if="list.length" class="bottom_btn" @click="golyform">我要留言</div>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
  export default {
    data () {
      return {
        list:[],
        userId:""
      }
    },

    created () {

    },
    methods:{
      golyform(){
        var that=this;
        wx.getStorage({
          key: 'userInfos',
          success(res) {
            wx.navigateTo({
              url:`/pages/lyform/main`
            });
          },
          fail(){
            wx.showToast({
              title: '请登录后重试',
              icon: 'none',
              duration: 2000
            })
          }
        })

      },
      getMyCommentList(Id){
        //console.log(Id)
        //获取我的评论列表
        var that=this;
        wx.request({
          url:`${conf.HOST}/stddj-gzgj/servlet/comment.action?method=getMyCommentList`,
          data:{
            userId:Id
          },
          success(res){
            //console.log(JSON.stringify(res.data))
            that.list=res.data;
          }
        })
      }
    },
    onLoad(params){
      this.userId=params.userId;
      // this.getMyCommentList(params.userId);
    },
    onShow(){
      this.getMyCommentList(this.userId);
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
 .wyly{
   width: 100%;
   height: 100vh;
   overflow: hidden;
   background: url("../../images/logo.png") no-repeat;
   background-size: 363rpx 70rpx;
   background-position: center bottom 30rpx;
   position: relative;
   .scroll{
     width: 100%;
     height: 100vh;
     overflow: hidden;
     background: #f3f6fd;
     padding-top:15rpx;
     box-sizing: border-box;
     padding-bottom: 108rpx;
   .lyb{
      .list{
        width: 690rpx;
        height: 194rpx;
        margin:0 30rpx;
        box-sizing: border-box;
        background: url("../../images/ly_list_bg.png") no-repeat;
        background-size:100%;
        padding:34rpx 40rpx;
        display: flex;
        margin-bottom: 20rpx;
        box-shadow:0 0 12rpx rgba(227,226,243,0.5);
        .info{
          width: 100%;
          flex:1;
          display: flex;
          flex-direction: column;
          justify-content: space-between;
          .title{
            font:30rpx "微软雅黑";
            color:#333333;
            text-overflow: -o-ellipsis-lastline;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            line-clamp: 2;
            -webkit-box-orient: vertical;
          }
          .time{
            font:22rpx "微软雅黑";
            color:#7f8699;
          }
        }
        .state{
          width:150rpx;
          display: flex;
          justify-content: flex-end;
          .btn{
            width: 120rpx;
            height: 60rpx;
            box-sizing: border-box;
            border-radius:10rpx;
            border:1rpx dashed #c3cced;
            font:22rpx "微软雅黑";
            line-height: 60rpx;
            color:#4d5068;
            text-align: center;
          }
          .ok{
            color: @mainColor;
            border-color: @mainColor;
          }
        }
      }
    }
   }
   .null{
     width: 100%;

     background: #fff;
     text-align: center;
     img{
       width: 384rpx;
       margin-top:332rpx;
       margin-bottom: 150rpx;
     }
     .btn{
       width: 384rpx;
       height: 88rpx;
       text-align: center;
       background: @mainColor;
       border-radius: 10rpx;
       color:#fff;
       margin:0 auto;
       font:34rpx "微软雅黑";
       line-height: 88rpx;
     }
   }
   .ly_btn{
     width:400rpx;
     height:88rpx;
     font:34rpx "微软雅黑";
     line-height: 88rpx;
     color:#fff;
     text-align: center;
     border-radius: 10rpx;
     background: @mainColor;
     margin: 0 auto;
   }
   .bottom_btn{
     width: 100%;
     height: 88rpx;
     color:#fff;
     background: @mainColor;
     text-align: center;
     font:34rpx "微软雅黑";
     line-height: 88rpx;
     position: absolute;
     bottom: 0;
     left: 0;
   }
 }
</style>
