<template>
  <div class="zddw">
    <scroll-view :scroll-y="true" class="scroll">
      <div class="content">
        <div class="jllist" v-if="list.length" v-for="(item,index) in list" :key="index">
          <img class="disimg" v-if="item.UNIT_THUMB_IMG" :src="item.UNIT_THUMB_IMG" @error="errorfn(index)">
          <div class="center"  @click="goDetail(item.UNIT_ID)">
            <div class="name">{{item.UNIT_NAME}}</div>
            <div>
              <div class="addr">{{item.DISTANCE}}km | {{item.UNIT_ADDR}}</div>
              <div class="tel">联系电话:{{item.UNIT_TEL}}</div>
            </div>
          </div>
          <div class="phone">
            <img src="../../images/phone.png" class="icon" @click="Call(item.UNIT_TEL)">
          </div>
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
        list:[]
      }
    },

    mounted () {
      this.getList();
    },
    methods:{
      getList(){
        var that=this;
        wx.getStorage({
          key: 'Location',
          success(ret) {
            // console.log(ret.data.lon+":"+ret.data.lat)
            wx.request({
              //获取重点单位列表
              url: conf.HOST+"/stddj-gzgj/servlet/unit.action?method=getUnitList",
              data: {
                lon:ret.data.lon,
                lat:ret.data.lat,
                pageNo:1,
                pageSize:10
              },
              header: {
                'content-type': 'application/json', // 默认值
                'Authorization':ret.data.token
              },
              success (res) {
                that.list=res.data;
              }
            });
          }
        })
      },
      goDetail(id){
        wx.navigateTo({
          url:`/pages/serverDetail/main?type=2&UNIT_ID=${id}`
        });
      },
      Call(number){
        wx.makePhoneCall({
          phoneNumber:number
        });
      },
      errorfn(index){
        this.list[index].NEWS_THUMB_IMG="../../images/default_img.jpg"
      }
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  .zddw{
    width: 100%;
    height: 100vh;
    overflow: hidden;
    .scroll{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
      .content{
        width: 680rpx;
        margin: 0 auto;
        background: #fff;
        .jllist{
          width: 100%;
          height: 174rpx;
          overflow: hidden;
          display: flex;
          align-items: center;
          position: relative;
          border-bottom:1rpx solid #f2f2f2;
          .disimg{
            width: 310rpx;
            height: 130rpx;
            margin-right: 30rpx;
            float: left;
            border-radius:10rpx;
          }
          .center{
            width: 100%;
            height: 130rpx;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            overflow: hidden;
            .name{
              font:30rpx "黑体";
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
            }
            .addr,.tel{
              width: 100%;
              font:20rpx "黑体";
              color:#7b8086;
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
            }
            .addr{
              margin-bottom: 10rpx;
            }
          }
          .phone{
            width:130rpx;
            height:130rpx;
            position: relative;
            float: right;
            margin-left: 50rpx;
            .icon{
              width: 86rpx;
              height: 50rpx;
              position: absolute;
              bottom: 6rpx;
              right: 10rpx;
            }
          }
        }
      }
    }
  }
</style>
