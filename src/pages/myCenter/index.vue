<template>
  <div class="myCenter">
    <div class="myCenter_container">
      <div class="card">
        <div class="top">
          <div>
            <div class="avatar">
              <open-data class="avatar" type="userAvatarUrl"></open-data>
            </div>
            <dl>
              <dt>{{userInfos.USER_NAME}}</dt>
              <dd>{{userInfos.ORG_NAME}}</dd>
            </dl>
          </div>
          <span v-if="!userInfos" @click="goDetail(`/pages/login/main`)">登录</span>
        </div>
        <div class="bottom">
          <dl>
            <dt>积分</dt>
            <dd>{{jfRank.bonusPoint}}</dd>
          </dl>
          <dl>
            <dt>排名</dt>
            <dd>{{jfRank.bonusRank}}</dd>
          </dl>
        </div>
      </div>
      <div class="list">
        <div class="list_item" @click="goDetail('/pages/jjb/main')">
          <div>
            <span class="iconfont1 icon-huiyishi12"></span>
            我的聚聚吧
          </div>
          <span> > </span>
        </div>
        <div class="list_item" @click="goDetail('/pages/volunteerActivty/main')">
          <div>
            <span class="iconfont1 icon-zhiyuan1"></span>
            我的志愿活动
          </div>
          <span> > </span>
        </div>
        <div class="list_item" @click="goDetail('/pages/zjdx/main')">
          <div>
            <span class="iconfont1 icon-xuexi1"></span>
            我的学习
          </div>
          <span> > </span>
        </div>
        <div class="list_item" @click="goDetail('/pages/myCollections/main')">
          <div>
            <span class="iconfont1 icon-shoucangxinxianshi1"></span>
            我的收藏
          </div>
          <span> > </span>
        </div>
        <div class="list_item" @click="goDetail('/pages/wyly/main')">
          <div>
            <span class="iconfont1 icon-liuyan-1"></span>
            我要留言
          </div>
          <span> > </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import * as conf from "../../utils/config"
  export default {

    data () {
      return {
        userInfos:{},
        jfRank:{}
      }
    },

    created () {

    },
    methods:{
      getUserInfo(){
        //获取个人信息
        var that=this;
        wx.getStorage({
          key: 'userInfos',
          success(ret) {
             //console.log(JSON.stringify(res.data));
             that.userInfos=ret.data;
             wx.request({
               url:`${conf.HOST}/eac-tvmodule//person.action?method=getPersonInfo`,
               data:{
                 USER_ID:ret.data.USER_ID
               },
               success(res){
                 that.jfRank=res.data;
               }
             })
          }
        })
      },
      goDetail(url){
        wx.navigateTo({
          url:url
        })
      }
    },
    onLoad(){
      this.getUserInfo();
    },
    components: {
    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  @import "../../common/css/less/base";
  .myCenter{
    width: 100%;
    .myCenter_container{
      width: 100%;
      padding:20rpx 30rpx;
      box-sizing: border-box;
      .card{
        width: 100%;
        height: 350rpx;
        padding:50rpx 40rpx;
        box-sizing: border-box;
        background: linear-gradient(to bottom,#FF332E,#F41919);
        box-shadow: 0 4rpx 10rpx rgba(232,44,44,0.5);
        -webkit-border-radius: 10rpx;
        -moz-border-radius: 10rpx;
        border-radius: 10rpx;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        margin-bottom:90rpx;
        .top{
          display: flex;
          align-items: center;
          color:#fff;
          >div{
            display: flex;
          }
          .avatar{
            width: 110rpx;
            height: 110rpx;
            border-radius: 50%;
            overflow: hidden;
            box-shadow: 4rpx 6rpx 2rpx rgba(0,0,0,.2);
            margin-right: 46rpx;
          }
          dl{
              display: flex;
              flex-direction: column;
              justify-content: center;
              margin-right: 50rpx;
            dt{
              font:600 32rpx "微软雅黑";
              margin-bottom: 10rpx;
            }
            dd{
              font:22rpx "黑体";
            }
          }
          span{
            display: block;
            width:100rpx;
            height:52rpx;
            background:rgba(212,3,3,0.6);
            border-radius:26rpx 26rpx 26rpx 26rpx;
            font:28rpx "微软雅黑";
            line-height: 52rpx;
            text-align: center;
            color:#fff;
          }
        }
        .bottom{
          display: flex;
          justify-content: space-between;
          color:#fff;
          dl{
            display: flex;
            justify-content: center;
            align-items: flex-end;
            flex: 1;
            dt{
              font:26rpx "微软雅黑";
              margin-right: 36rpx;
            }
            dd{
              font:60rpx "微软雅黑";
            }
          }
        }
      }
      .list{
        padding:0 50rpx;
        .list_item{
          width: 100%;
          display: flex;
          align-items: center;
          justify-content: space-between;
          font:30rpx "微软雅黑";
          color:#333;
          margin-bottom: 88rpx;
          div{
            display: flex;
            align-items: center;
            span:first-child{
              color: @mainColor;
              margin-right: 20rpx;
            }

          }
          span:last-child{
            font-family: "宋体";
            color:#C3CCED;
            font-size:30rpx;
            font-weight: bold;
          }
        }
      }
    }
  }
</style>
