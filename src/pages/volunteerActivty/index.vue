<template>
  <div class="volunteerAct">
    <scroll-view class="scroll" :scroll-y="true">
      <div class="searchBox">
        <div class="search">
          <div class="addr"><i class="iconfont icon-dingwei"></i><span>江南中街道</span></div>
          <div class="input_area">
            <i class="iconfont icon-sousuo1"></i>
            <input type="text" :placeholder="placeholder" v-model="inputVal" @input="confirm($event)">
          </div>
        </div>
        <div class="content">
          <div class="btnGroups">
            <div class="btn" v-if="!volunteerInfos.success" @click="apply">{{volunteer}}</div>
            <div class="btn" v-if="volunteerInfos.success" @click="goMyZys">我的志愿时</div>
            <div class="btn" @click="goCalendar">活动日历</div>
          </div>
        </div>
      </div>
      <div class="cards" v-if="cardlist.length">
        <div class="content">
          <div class="cardlist"
               @click="goDetail(item.ACTIVITY_ID)"
               v-for="(item,index) in cardlist"
               :key="index"
               v-if="index<6">
            <div class="pic">
              <img :src="item.ACTIVITY_IMG" alt="" class="banner">
              <span>{{item.CUR_STATUS}}</span>
            </div>
            <div class="cont">
              <div><p>{{item.ACTIVITY_NAME}}</p><i class="iconfont icon-huo"></i></div>
              <dl>
                <dt><i class="iconfont icon-dingwei1"></i>{{item.ACTIVITY_ADDR}}</dt>
                <dd><i class="iconfont icon-shijian"></i>{{item.ACTIVITY_START}}</dd>
              </dl>
            </div>
          </div>
        </div>
      </div><!--卡片END-->
      <div class="past" v-if="pastlist.length">
        <div class="content">
          <div class="title">往期志愿活动</div>
          <div class="actlist" v-for="(item,index) in pastlist" :key="index" v-if="index<2" @click="goDetail(item.ACTIVITY_ID)">
            <div class="pic">
              <img :src="item.ACTIVITY_IMG" alt="">
              <span>{{item.CUR_STATUS}}</span>
              <div class="text">{{item.ACTIVITY_CLASS_NAME}}</div>
            </div>
            <div class="info">
              <p>
                {{item.ACTIVITY_NAME}}
              </p>
              <dl>
                <dt><i class="iconfont icon-dingwei1"></i>{{item.ACTIVITY_ADDR}}</dt>
                <dd>
                  <span><i class="iconfont icon-shijian"></i>{{item.ACTIVITY_START}}</span>
                  <!--<span><i class="iconfont icon-gengduo"></i>志愿活动</span>-->
                </dd>
              </dl>
            </div>
          </div>
        </div>
      </div><!--服务公告END-->
    </scroll-view>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
  // import {ajax} from '../../utils/index'
  export default {

    data () {
      return {
        placeholder:"搜索精彩活动",
        volunteer:"志愿活动",
        cardlist:[],
        pastlist:[],
        volunteerInfos:{}
      }
    },
    onLoad() {
      this.cardList();
      this.pastList();
      this.getvolunteerInfos();
    },
    onUnload(){
      this.inputVal="";
      this.pastlist=[];
    },
    methods:{
      cardList(){//获取热门活动
        var that=this;
        wx.request({
          url: conf.HOST+`/cloud-app/activity.action?method=getActivityList&ACTIVITY_STATUS=1&curStatus=3&pageSize=2&pageNo=1`,
          data:{},
          header: {
            'content-type': 'application/json'
          },
          success (res) {
            // console.log(JSON.stringify(res.data));
            that.cardlist=res.data;
          }
        });
      },
      pastList(){
        var that=this;
        wx.request({
          url: conf.HOST+`/cloud-app/activity.action?method=getActivityList&ACTIVITY_STATUS=1&curStatus=2&pageSize=2&pageNo=1`,
          data:{},
          header: {
            'content-type': 'application/json'
          },
          success (res) {
            // console.log(JSON.stringify(res.data));
            that.pastlist=res.data;
          }
        });
      },
      confirm(e){
        //搜索获取全部活动列表
        //console.log(e.target.value)
        this.inputVal=e.target.value
        //console.log(this.inputVal);
        var that=this;
        if(this.inputVal){
          wx.request({
            url:`${conf.HOST}/cloud-app/activity.action?method=getActivityList&ACTIVITY_STATUS=1`,
            data:{
              ACTIVITY_STATUS:1,
              pageSize:2,
              pageNo:1,
              ACTIVITY_NAME:that.inputVal
            },
            success(res){
              //console.log(JSON.stringify(res.data));
              if(res.data.length){
                wx.setStorage({
                  key: 'searchList',
                  data:res.data,
                  success(){
                    wx.navigateTo({
                      url:`/pages/searchActivty/main`
                    })
                  }
                })
              }else{
                wx.showToast({
                  title:"未搜索到相关数据",
                  icon:"none",
                  duration:2000
                })
              }
            }
          })
        }

      },
      goDetail(id){
        console.log(id)
        wx.getStorage({
          key:"userInfos",
          success(ret){
            wx.navigateTo({
              url:`/pages/outLink/main?type=0&ACTIVITY_ID=${id}&USER_CODE=${ret.data.USER_CODE}&USER_ID=${ret.data.USER_ID}`
            });
          },
          fail(){
            wx.showToast({
              title:"请登录后重试",
              icon:"none",
              duration:2000
            })
          }
        })
      },
      apply(){
        //申请成为志愿者
        wx.navigateTo({
          url:`/pages/applyVolunteer/main`
        })
      },
      getvolunteerInfos(){
        var that=this;
        //获取志愿时长
        wx.getStorage({
          key: 'userInfos',
          success(ret) {
            //console.log(ret.data);
            wx.request({
              url:`${conf.HOST}/eac-tvmodule/RegistUser.action?method=getVolunUser`,
              data:{
                USER_ID:ret.data.USER_ID
              },
              success(res){
                //console.log(JSON.stringify(res.data));
                that.volunteerInfos=res.data;
              }
            })
          },
          fail(){
            wx.showToast({
              title:"请登录后重试",
              icon:"none",
              duration:2000
            })
          }
        })
      },
      goCalendar(){
        wx.navigateTo({
          url:`/pages/volunteerCalendar/main`
        })
      },
      goMyZys(){
        wx.navigateTo({
          url:`/pages/volunteerTimeList/main`
        })
      }
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  .volunteerAct{
    width: 100%;
    position: relative;
    .scroll{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
    }
    .searchBox{
      display: flex;
      flex-direction: column;
      .search{
        width: 100%;
        height: 96rpx;
        background: #fff;
        padding:26rpx 20rpx;
        display: flex;
        align-items: center;
        justify-content: space-between;
        box-sizing: border-box;
        .addr{
          display: flex;
          align-items: center;
          color:#7f8699;
          i{
            margin-left:-18rpx;
          }
          span{
            font:28rpx "黑体";
          }
        }
        .input_area{
          width: 508rpx;
          height: 60rpx;
          background:#f7f8fc;
          border-radius: 10rpx;
          padding-left: 32rpx;
          padding-right: 70rpx;
          box-sizing: border-box;
          display: flex;
          align-items: center;
          position: relative;
          input{
            width: 100%;
            font:28rpx "黑体";
            line-height:60rpx;
          }
          input::placeholder{
            color:#bfbfbf;
          }
          i{
            position: absolute;
            right:22rpx;
            color:#bfbfbf;
          }
        }
      }

      .btnGroups{
        width: 100%;
        display: flex;
        justify-content:space-around;
        padding-bottom: 26rpx;
        .btn{
          width: 326rpx;
          height:82rpx;
          border:1rpx solid #f2f2f2;
          border-radius: 10rpx;
          font:30rpx "微软雅黑";
          line-height: 82rpx;
          text-align: center;
          color:#4d5068;
        }
      }
    }
    .cards{
      background: #f6f8fd;
      padding:20rpx 0;
      .cardlist{
        width: 100%;
        border-radius:10rpx;
        margin-bottom: 20rpx;
        overflow: hidden;
        background: #fff;
        .pic{
          width: 100%;
          height: 226rpx;
          position: relative;
          .banner{
            width: 100%;
            height: 226rpx;
          }
          span{
            display: block;
            width: 100rpx;
            height: 40rpx;
            font:20rpx "黑体";
            line-height: 40rpx;
            background: #d40303;
            color:#fff;
            text-align: center;
            position: absolute;
            right: 24rpx;
            top:0;
            border-radius:0 0 10rpx 10rpx;
          }
        }
        .cont{
          padding:22rpx;
          box-sizing: border-box;
          >div{
            margin-bottom: 16rpx;
            display: flex;
            p{
              width: 508rpx;
              height: 40rpx;
              line-height: 40rpx;
              font:30rpx "微软雅黑";
              color:#333;
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
            }
          }
          dl{
            font:22rpx "黑体";
            color:#7f8699;
            dt{
              display: flex;
              align-items: center;
              margin-bottom: 5rpx;
              i{
                margin-left: -16rpx;
                color:#bec4d3;
              }
            }
            dd{
              display: flex;
              align-items: center;
              i{
                font-size: 22rpx;
                margin-right: 20rpx;
                color:#bec4d3;
              }
            }
          }
        }
        .icon-huo{
          color:#d81e06;
          margin-left: 10rpx;
        }
      }
      .cardlist:last-child{
        margin-bottom: 0;
      }
    }
    .past{
      background: #fff;
      .actlist{
        display: flex;
        padding:0 20rpx;
        padding-bottom: 30rpx;
        margin-bottom: 30rpx;
        border-bottom:1rpx solid #f2f2f2;
        box-sizing: border-box;
        .pic{
          position: relative;
          width: 230rpx;
          height: 150rpx;
          border-radius:8rpx;
          margin-right: 26rpx;
          overflow: hidden;
          img{
            width: 230rpx;
            height: 150rpx;
          }
          span{
            display: block;
            width: 86rpx;
            height: 30rpx;
            font:22rpx "黑体";
            text-align: center;
            color:#fff;
            background: #d40303;
            border-radius:0 0 6rpx 6rpx;
            position: absolute;
            top:0;
            left: 16rpx;
          }
          .text{
            width: 100%;
            height: 30rpx;
            font:22rpx "黑体";
            background: rgba(0,0,0,0.5);
            color:#fff;
            text-align: center;
            position: absolute;
            left: 0;
            bottom: 0;
          }
        }
        .info{
          flex:1;
          p{
            font:30rpx "黑体";
            color:#333;
            height: 76rpx;
            line-height: 39rpx;
            overflow: hidden;
            position: relative;
            margin-bottom: 12rpx;
          }
          dl{
            color:#999999;
            dt{
              font:22rpx "黑体";
              display: flex;
              height:30rpx;
              overflow: hidden;
              margin-bottom: 2rpx;
              .icon-dingwei1{
                font-size: 28rpx;
                margin-right:10rpx;
                margin-left:-13rpx;
              }
            }
            dd{
              display: flex;
              font:22rpx "黑体";
              span{
                display: flex;
                align-items: center;
              }
              span:first-child{
                display: flex;
                margin-right: 30rpx;
              }
            }
            i{
              font-size: 22rpx;
              margin-right: 20rpx;
            }
            .icon-gengduo{
              font-size: 14rpx;
            }
          }
        }
      }
      .title{
        width: 100%;
        font:32rpx "黑体";
        height:120rpx;
        line-height: 120rpx;
        font-weight: bold;
        color:#000;
        padding:0 20rpx;
        box-sizing: border-box;
      }
    }
    .content{
      width: 712rpx;
      margin:0 auto;
    }
  }
</style>
