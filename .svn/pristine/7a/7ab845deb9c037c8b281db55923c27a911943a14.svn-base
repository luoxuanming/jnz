<template>
  <div class="power">
    <div class="head">
      <img src="../../images/power.png" alt="" class="power_img">
      <div class="tab">
        <div class="btnGroups">
          <div class="btn" :class="current==0?'active':' '" @click="changelist(0)">先进人物</div>
          <div class="btn" :class="current==1?'active':' '" @click="changelist(1)">身边好人</div>
        </div>
      </div>
    </div>
    <scroll-view :scroll-y="true" class="scroll">
      <div class="content" >
        <div class="list" v-for="(item,index) in powerList" :key="index" @click="goNewsDetail(item.NEWS_ID)">
          <img :src="item.NEWS_THUMB_IMG" alt="">
          <dl>
            <dt>{{item.NEWS_AUTHOR}}</dt>
            <dd>{{item.SUB_TITLE}}</dd>
          </dl>
        </div>
      </div>
    </scroll-view>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'

export default {
  data () {
    return {
      powerList:[],
      current:0,
      xjrwID:"",
      sbhrID:""
    }
  },
  methods:{
    initPowerList(id){
      console.log(id);
      var that=this;
      this.HOST=conf.HOST;
      wx.request({
        url: conf.HOST+"/cloud-app/servlet/dynamic.action?method=getChannel",
        data: {
          CHANNEL_ID:id,
          orgId:1
        },
        header: {
          'content-type': 'application/json' // 默认值
        },
        success (res) {
          that.xjrwID=res.data[0].CHANNEL_ID;//先进人物CHANNEL_ID
          that.sbhrID=res.data[1].CHANNEL_ID;//身边好人CHANNEL_ID
          // that.$nextTick(function(){
          //   that.powerList=res.data;
          //   console.log(that.powerList)
          // })
          that.getList(that.xjrwID);
        }
      });
    },
    goNewsDetail(id){
      wx.navigateTo({
        url:`/pages/newsDetail/main?newsId=`+id
      });
    },
    changelist(index){
      this.current=index;
      if(this.current==0){
        this.getList(this.xjrwID);
      }else{
        this.getList(this.sbhrID);
      }
    },
    getList(id){
      var that=this;
      wx.request({
        url:`${conf.HOST}/cloud-app/servlet/dynamic.action?method=getDynamicByChannel`,
        data:{
          CHANNEL_ID:id
        },
        success(res){
          that.powerList=res.data;
        }
      })
    }
  },
  created () {

  },
  onLoad:function(id){
    let {CHANNEL_ID}=id;
    this.initPowerList(CHANNEL_ID);
  },
  components: {

  }
}
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  .power{
    .head{
      position: fixed;
      width: 100%;
      height: 432rpx;
      top:0;
      left: 0;
      background: #fff;
      z-index: 99;
      .tab{
        width: 100%;
        height: 110rpx;
        position: absolute;
        left:0;
        bottom: 0;
        display: flex;
        justify-content: center;
        .btnGroups{
          width: 462rpx;
          height: 64rpx;
          border-radius: 10rpx;
          border:1rpx solid rgba(212,3,3,.6);
          box-shadow:0 0 6rpx rgba(212,3,3,.3);
          display: flex;
          overflow: hidden;
          .btn{
            font:30rpx "微软雅黑";
            color:#4d5068;
            flex:1;
            background: #fff;
            text-align: center;
            line-height: 64rpx;
          }
          .active{
            background: rgba(212,3,3,1);
            color:#fff;
          }
        }
      }
      .power_img{

        width: 100%;
        height: 288rpx;
        margin-bottom: 22rpx;
      }
    }
    .scroll{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
      .content{
        padding:0 40rpx;
        background: #fff;
        padding-top:434rpx;
        .list{
          width:100%;
          height: 209rpx;
          background: #f3f6fd;
          border-radius:10rpx;
          display: flex;
          padding:20rpx;
          box-sizing: border-box;
          margin-bottom: 22rpx;
          img{
            width: 284rpx;
            height: 168rpx;
            border-radius: 10rpx;
            box-shadow:0 8rpx 5rpx rgba(154,167,213,0.6);
            margin-right: 24rpx;
          }
          dl{
            width: 314rpx;
            height: 168rpx;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            overflow: hidden;
            dt{
              font:38rpx "黑体";
              font-weight: bold;
              color:#333333;
            }
            dd{
              font:28rpx "微软雅黑";
              color:#4d5068;
            }
          }
        }
      }
    }
  }
</style>
