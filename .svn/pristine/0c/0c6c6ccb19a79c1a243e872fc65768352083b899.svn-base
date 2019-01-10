<template>
  <div class="tab">
    <div class="content">
      <scroll-view class="scroll" :scroll-x="true">
        <ul>
          <li v-for="(item,index) in channellist"
              :key="index"
              :class="current==item.CHANNEL_ID?'current':''"
              @click="change(item.CHANNEL_ID)">{{item.CHANNEL_NAME}}
          </li>
        </ul>
      </scroll-view>
    </div>

    <div class="list" @click="goNewsDetail(item.NEWS_ID)" v-for="(item,index) in newlist" :key="index">
      <dl>
        <dt>{{item.MAIN_TITLE}}</dt>
        <dd>
          <span>{{item.MODIFY_TIME}}</span>
          <span class="count">{{item.READ_COUNT}} 阅读</span>
        </dd>
      </dl>
      <img v-if="item.NEWS_THUMB_IMG!=null" :src="item.NEWS_THUMB_IMG" @error="errorfn(index)" alt="" class="listimg">
    </div>
    <div v-if="!newlist.length" class="" style="font:28rpx '黑体';color:#7f8699;text-align: center; padding:20rpx 0">暂无数据</div>
    <!--<div class="list" @click="goNewsDetail()" v-for="(item,index) in newlist" :key="index">
      <dl>
        <dt>深圳开发开发40年深圳开发开发40年深圳开发开发40年深圳开发开发40年深圳开发开发40年</dt>
        <dd>
          <span>2018/09/15 17:00</span>
          <span class="count">2323 阅读</span>
        </dd>
      </dl>
    </div>-->
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
    export default {
      data(){
        return{
          current:110032,
          newlist:[]
        }
      },
      props:{
        channellist:{
          type:Array,
          require:true
        }
      },
      methods:{
        change(index){
          this.current=index;
          this.getNewList();
        },
        getNewList(){
          var _this=this;

          wx.request({
            url: conf.HOST+"/cloud-app/servlet/dynamic.action?method=getDynamicByChannel",
            data: {
              CHANNEL_ID:_this.current,
              pageIndex:1,
              pageSize:10
            },
            header: {
              'content-type': 'application/json' // 默认值
            },
            success (res) {
              // console.log(JSON.stringify(res.data));
              _this.$nextTick(function(){
                _this.newlist=res.data;
              })
            }
          });
        },
        goNewsDetail(id){
          wx.navigateTo({
            url:`/pages/newsDetail/main?newsId=`+id
          });
        },
        errorfn(index){
          this.newlist[index].NEWS_THUMB_IMG="../../images/default_img.jpg"
        }
      },
      created () {
        this.getNewList();
      }
    }
</script>

<style scoped lang="less">
  .tab{
    width:100%;
    padding:18rpx 0;
    background: #fff;
    min-height:400rpx;

    .content{
      width:100%;
      height:70rpx;
      border-bottom:1rpx solid #f2f2f2;
      .scroll{
        width: 100%;
        height: 70rpx;
        overflow: hidden;
      }
      ul{
        height:70rpx;
        margin:0 auto;
        white-space: nowrap;
        li{
          width: 22.2%;
          height:70rpx;
          font:30rpx "微软雅黑";
          line-height:70rpx;
          color:#7f8699;
          text-align:center;
          position:relative;
          display: inline-block;
        }
        li::before{
          position:absolute;
          content: '';
          width:50rpx;
          height:4rpx;
          background:transparent;
          bottom:0;
          left:70rpx;
        }
        .current{
          font:35rpx "黑体";
          font-weight:bold;
          letter-spacing: -2rpx;
          line-height:70rpx;
          color:#000;
        }
        .current::before{
          background:#ea0000;
        }
      }
    }
  }
  .list{
    width:692rpx;
    margin:0 auto;
    display: flex;
    align-items:center;
    justify-content: space-between;
    height:178rpx;
    box-sizing:border-box;
    padding:24rpx 0;
    background: #fff;
    border-bottom: 1rpx solid #f2f2f2;
    overflow: hidden;
    dl{
      width:100%;
      box-sizing: border-box;
      overflow: hidden;
      dt{
        height: 90rpx;
        font:30rpx "微软雅黑";
        margin-bottom:10rpx;
        text-align: justify;
        overflow: hidden;
      }
      dd{
        span{
          font:24rpx "黑体";
          color:#7f8699;
        }
        .count{
          margin-left:36rpx;
        }
      }
    }
    .listimg{
      width:276rpx !important;
      height:123rpx;
      margin-left:80rpx;
      box-sizing: border-box;
    }
  }
</style>
