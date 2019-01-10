<template>
  <div class="volunteerTimeList">
    <scroll-view :scroll-y="true" class="scroll" v-if="list.length">
      <div class="TimeList_container">
        <div class="list" v-for="(item,index) in list" :key="index">
          <div class="left">
            <div class="time">
              <dl>
                <dt>{{item.ACTIVITY_START.substr(8,2)}}</dt>
                <dd>{{item.ACTIVITY_START.substr(0,7)}}</dd>
              </dl>
            </div>
            <div class="tag">+{{item.VOLUNTEER_TIME}}志愿时</div>
          </div>
          <div class="right">
            <img src="../../images/default_img.jpg" alt="">
            <dl>
              <dt>
                {{item.ACTIVITY_NAME}}
              </dt>
              <dd><i class="iconfont icon-gengduo1"></i>{{item.ACTIVITY_CLASS_NAME}}</dd>
            </dl>
          </div>
        </div>
      </div>
    </scroll-view>
    <div class="kong" v-if="!list.length">
      <img src="../../images/ly_null0.png" alt="">
      <div class="msg">暂无数据</div>
    </div>
  </div>
</template>

<script>
  import * as conf from "../../utils/config"
  export default {

    data () {
      return {
        list:[1,1,1,1]
      }
    },
    methods:{
    getUserApplyActivityList(){
      //获取志愿时长列表
      var that=this;
      wx.getStorage({
        key: 'userInfos',
        success(ret) {
          wx.request({
            url:`${conf.HOST}/cloud-app/activity.action?method=getUserApplyActivityList`,
            data:{
              USER_CODE:ret.data.USER_CODE
            },
            success(res){
              // console.log(JSON.stringify(res.data))
              that.list=res.data;
            }
          })
        }
      })

    }
    },
    onLoad(){
      this.getUserApplyActivityList();
    },
    created () {

    },
    components: {
    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  @import "../../common/css/font/iconfont.css";
  .volunteerTimeList{
    width: 100%;
    height: 100vh;
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
    .scroll{
      width: 100%;
      height: 100vh;
      box-sizing: border-box;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
      .list{
        width: 100%;
        height: 170rpx;
        background: url("../../images/zysc_list.png") no-repeat;
        background-size: 100% 100%;
        display: flex;
        margin-bottom: 10rpx;
        .left{
          width: 148rpx;
          height: 100%;
          position: relative;
          .time{
            dl{
              color:#333;
              text-align: center;
              padding-top:18rpx;
              dt{
                font:38rpx "黑体";
              }
              dd{
                font:22rpx "黑体";
              }
            }
          }
          .tag{
            width: 122rpx;
            height: 40rpx;
            border-radius: 0 10rpx 10rpx 0;
            background: @mainColor;
            font:22rpx "黑体";
            color:#fff;
            position: absolute;
            left: 6rpx;
            bottom:26rpx;
            line-height: 40rpx;
            text-align: center;
          }
        }
        .right{
          flex:1;
          height: 100%;
          display: flex;
          overflow: hidden;
          align-items: center;
          padding-left:16rpx;
          padding-bottom: 6rpx;
          padding-right: 10rpx;
          box-sizing: border-box;
          img{
            width:194rpx;
            height:126rpx;
            border-radius:4rpx;
            margin-right: 20rpx;
          }
          dl{
            flex:1;
            overflow: hidden;
            color:#333;
            dt{
              font:30rpx "微软雅黑";
              margin-bottom: 5rpx;
              text-overflow: -o-ellipsis-lastline;
              overflow: hidden;
              text-overflow: ellipsis;
              display: -webkit-box;
              -webkit-line-clamp: 2;
              line-clamp: 2;
              -webkit-box-orient: vertical;
            }
            dd{
              font:22rpx "黑体";
              display: flex;
              align-items: center;
              i{
                font-style: 12rpx;
                margin-left: -12rpx;
              }
            }
          }
        }
      }
      .TimeList_container{
        width: 100%;
        padding:0 24rpx;
        box-sizing: border-box;
      }
    }
  }
</style>
