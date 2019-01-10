<template>
  <div class="ldbywy">
    <div class="head">
      <img src="../../images/ldbywy.png" class="ldbywy_bg" alt="" @click="goAnswer">
      <div class="head_btn" @click="goAnswer">什么是两代表一委员？</div>
    </div>
    <scroll-view class="scroll" :scroll-y="true">
      <div class="content">
        <ul class="list">
          <li v-if="list.length" v-for="(item,index) in list" :key="index">
            <div class="pic" @click="goDetail(item.REPRESENT_ID)">
              <img v-if="item.REPRESENT_THUMB_IMG==null" src="../../images/default_img.jpg" class="photo" alt="">
              <img v-if="item.REPRESENT_THUMB_IMG!=null" :src="item.REPRESENT_THUMB_IMG" class="photo" alt="">
            </div>
           <div class="js">
             <p>{{item.REPRESENT_USER_NAME}}</p>
             <div class="head_btn" @click="goWyly(item.REPRESENT_ID)">给Ta留言</div>
           </div>
          </li>
        </ul>
      </div>
    </scroll-view>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        list:[]
      }
    },

    created () {
      this.getlist();
    },
    methods:{
      goDetail(id){
        wx.navigateTo({
          url:`/pages/ldbywyDetail/main?representId=${id}`
        });
      },
      goWyly(repId){
        wx.navigateTo({
          url:`/pages/lyform/main?repId=${repId}`
        });
      },
      goAnswer(){
        wx.request({
          url:`${conf.HOST}/stddj-gzgj/servlet/represent.action?method=getRepresentNews`,
          data:{},
          header: {
            'content-type': 'application/json' // 默认值
          },
          success(res){
            wx.navigateTo({
              url:`/pages/newsDetail/main?newsId=`+res.data[0].NEWS_ID
            })
          }
        })
      },
      getlist(){
        var that=this;
        wx.getStorage({
          key: 'token',
          success(ret) {
            wx.request({
              url:`${conf.HOST}/stddj-gzgj/servlet/represent.action?method=getRepresentList`, // 仅为示例，并非真实的接口地址
              data: {
                userId: '2',
                orgId: '1'
              },
              header: {
                'content-type': 'application/json', // 默认值
                'Authorization':ret.data
              },
              success(res) {
                that.list=res.data;
              }
            })
          }
        })
      }
    },
    components: {
    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  .ldbywy{
    width: 100%;
    height:100vh;
    overflow: hidden;
    .head{
      width: 100%;
      height: 320rpx;
      position: fixed;
      top:0;
      left: 0;
      z-index: 999;
      .ldbywy_bg{
        width: 100%;
        height: 320rpx;
      }
      .head_btn{
        padding:10rpx 16rpx;
        background: rgba(255,255,255,.86);
        color:@mainColor;
        font:22rpx "黑体";
        position: absolute;
        right:52rpx;
        bottom: 140rpx;
        border-radius: 10rpx;
      }
    }
    .scroll{
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
      .list{
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        li{
          width: 320rpx;
          height: 484rpx;
          background: #f3f6fd;
          border-radius: 10rpx;
          padding:20rpx;
          box-sizing: border-box;
          margin-bottom: 20rpx;
          div.pic{
            width: 100%;
            height: 368rpx;
            border-radius: 10rpx;
            box-shadow:0 8rpx 5rpx rgba(154,167,213,0.6);
            overflow: hidden;
            margin-bottom: 20rpx;
            .photo{
              width: 100%;
              height: 100%;
            }
          }
          .js{
            display: flex;
            align-items: center;
            justify-content: space-between;
            .head_btn{
              padding:10rpx 16rpx;
              background: rgba(232,44,44,.86);
              color:@mainColor;
              font:22rpx "黑体";
              border-radius: 10rpx;
              color:#fff;
            }
          }
          p{
            font:30rpx "微软雅黑";
            color:#333;
          }
        }
      }
    }
    .content{
      width: 100%;
      padding:0 40rpx;
      box-sizing: border-box;
      padding-top:356rpx;
    }
  }
</style>
