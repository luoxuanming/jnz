<template>
  <div class="jjb">
    <scroll-view :scroll-y="true" class="scroll">
      <div class="state">
        <div class="content">
          <div class="circle">
            <i class="iconfont icon-loudou active"></i>
            <dl>
              <dt>进行中</dt>
              <dd>选择发起类型</dd>
            </dl>
          </div>
          <div class="default_line"></div>
          <div class="circle">
            <i class="iconfont icon-icon-test"></i>
            <dl>
              <dt>未开始</dt>
              <dd>填写信息并发起</dd>
            </dl>
          </div>
          <!--<div class="circle">
            <i class="iconfont icon-loudou"></i>
            <dl>
              <dt>已回复</dt>
              <dd>2018-07-01 10:00</dd>
            </dl>
          </div>-->
        </div>
      </div><!--状态END-->
      <div class="hr"></div>
      <div class="fq_type">
        <div class="content">
          <h4>选择发起类型</h4>
          <dl class="list" v-for="(item,index) in list" :key="index">
            <dt>{{item.type}}</dt>
            <dd>
              <i v-if="item.flag==true" class="iconfont icon-xuanzhonggou" @click="select(index)"></i>
              <i v-if="item.flag==false" class="border" @click="select(index)"></i>
            </dd>
          </dl>
        </div>
      </div><!--选择发起类型-->
      <div class="btn_groups content">
        <div class="btns">
          <div @click="preStep">上一步</div>
          <div @click="nextStep">下一步 <i class="iconfont icon-xuanzhonggou"></i> </div>
          <!--<div>发布 <i class="iconfont icon-fabu"></i> </div>-->
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
        index:0,
        list:[
          {
            type:"普通话题",
            flag:false,
            typeId:1
          },
          {
            type:"党员大会",
            flag:false,
            typeId:2
          },
          {
            type:"支委会",
            flag:false,
            typeId:3
          },
          {
            type:"党课",
            flag:false,
            typeId:4
          },
          {
            type:"投票评议",
            flag:false,
            typeId:5
          },
          {
            type:"活动",
            flag:false,
            typeId:6
          }
        ],
        listShu:''
      }
    },

    created () {

    },
    methods:{
      bindPickerChange(e){
        // console.log(e.target.value)
        this.index=e.target.value;
      },
      bindPickerChange2(e){
        // console.log(e.target.value)
        this.index2=e.target.value;
      },
      bindPickerChange3(e){
        // console.log(e.target.value)
        this.index3=e.target.value;
      }, 
      nextStep(){
        var that=this;
        that.listShu =''
        for(var i=0;i<that.list.length;i++){
          
         if(that.list[i].flag){
              if(that.listShu!=''){
                 
                 that.listShu=that.listShu+','+that.list[i].typeId
              }else{
                  that.listShu=that.list[i].typeId
              }
              
          }
        }
        if(that.listShu==''){
          that.listShu='1';
           wx.showModal({
            title: '提示',
            content: '没有选择发起类型,是否发起普通话题',
            success(res) {
              if (res.confirm) {
                 wx.navigateTo({
                    url:`/pages/jjbfq2/main?type=`+that.listShu
                  })
              } else if (res.cancel) {
                console.log('用户点击取消')
              }
            }
          })
          return false;
        }else if(that.list[3].flag){
          wx.showModal({
            title: '提示',
            content: '党课发起开发中,是否发起普通话题',
            success(res) {
              if (res.confirm) {
                 wx.navigateTo({
                    url:`/pages/jjbfq2/main?type=`+that.listShu
                  })
              } else if (res.cancel) {
                console.log('用户点击取消')
              }
            }
          })
       }else if(that.list[4].flag){
        
          wx.showModal({
            title: '提示',
            content: '投票评议发起开发中,是否发起普通话题',
            success(res) {
              if (res.confirm) {
                 wx.navigateTo({
                    url:`/pages/jjbfq2/main?type=`+that.listShu
                  })
              } else if (res.cancel) {
                console.log('用户点击取消')
              }
            }
          })
       }else{
          wx.navigateTo({
            url:`/pages/jjbfq2/main?type=`+that.listShu
          })
       }
        /*
        wx.navigateTo({
          url:`/pages/jjbfq2/main`
        })
        if(that.listShu!=''){
                  that.listShu=that.listShu+','+stthat.list[i].typeId
              }else{
                  that.listShu=stthat.list[i].typeId
              }
        */
      },
      preStep(){
        wx.navigateBack({
          delta:1
        })
      },
      select(index){
        this.list[index].flag=!this.list[index].flag;
      }
    },
    components: {
    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  @import "../../common/css/font/iconfont.css";
  .jjb{
    width: 100%;
    height: 100vh;
    overflow: hidden;
    .content{
      width: 100%;
      padding:0 40rpx;
      box-sizing: border-box;
    }
    .h4{
      width: 100%;
      height:112rpx;
      font:38rpx "黑体";
      font-weight:bold;
      line-height:112rpx;
      letter-spacing:-2rpx;
      margin-bottom: 10rpx;
    }
    .icon-xuanzhonggou{
      font-size: 42rpx;
      color:#f65d5d;
    }
    .hr{
      width: 100%;
      height: 20rpx;
      background: #f6f8fd;
    }
    .scroll {
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
    }
    .state {
      background: #fff;
      width: 100%;
      height: 190rpx;
      display: flex;
      align-items: center;
      .circle {
        display: flex;
        .iconfont {
          font-size: 96rpx;
          margin-right: 24rpx;
          color: #7f8699;
        }
        .active{
          color: #79ceff;
        }
        .icon-loudou {

        }
        dl {
          display: flex;
          flex-direction: column;
          justify-content: center;
          dt {
            font: 30rpx "微软雅黑";
            color: #333;
            margin-bottom: 10rpx;
          }
          dd {
            font: 22rpx "微软雅黑";
            color: @smfontColor;
          }
        }
      }
      .line {
        width: 88rpx;
        height: 2rpx;
        background: #79ceff;
      }
      .default_line {
        width: 88rpx;
        height: 2rpx;
        background: #7f8699;
      }
      > .content {
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
    }
    .fq_type,.info{
      width: 100%;
      background:#fff;
      padding:30rpx 0;
      padding-bottom: 0;
    }
    .list{
      width: 100%;
      height: 83rpx;
      border-bottom:1rpx solid #f2f2f2;
      display: flex;
      align-items: center;
      justify-content: space-between;
      dt{
        font:30rpx "微软雅黑";
        color:#333;
        .xing{
          color:#f65d5d;
          margin-left: 10rpx;
        }
      }
      dd{
        .border{
          display: block;
          width: 40rpx;
          height: 40rpx;
          border:1rpx solid #cdcdcd;
          border-radius:20rpx;
          box-sizing: border-box;
        }
        .picker{
          font:30rpx "微软雅黑";
          color:#333;
          display: flex;
          align-items: center;
          .icon-xiala{
            margin-left: 12rpx;
            font-size: 26rpx;
          }
        }
        .moren{
          color:#cccccc;
        }
        input{
          font:30rpx "微软雅黑";
        }
        input::-moz-placeholder{
          color:#ccc;
        }
      }
    }
    .list:last-child{
      border:none;
    }
    .zt{
      height: 130rpx !important;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;
      dt{
        margin-bottom: 10rpx;
      }
      dd{}
    }
    .fj{
      width: 100%;
      height: 80rpx;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #fff;
      div{
        height: 80rpx;
        font:30rpx "微软雅黑";
        color:#333;
        padding:0 40rpx;
        height: 80rpx;
        display: flex;
        align-items: center;
        img{
          width: 50rpx;
          height: 50rpx;
          margin-right: 20rpx;
        }
      }
      .icon{
        color:#d7dce9;
        font-size: 66rpx;
      }
    }
    .btn_groups{
      width: 100%;
      padding-top:22rpx;
      /*background: #f6f8fd;*/
      span{
        display: block;
        font:32rpx "微软雅黑";
        color:#97abf4;
        margin-bottom: 80rpx;
      }
      .btns{
        display: flex;
        justify-content: space-between;
        div{
          width: 320rpx;
          height: 88rpx;
          background: #97abf4;
          color:#fff;
          font:30rpx "微软雅黑";
          line-height: 88rpx;
          border-radius: 10rpx;
          display: flex;
          justify-content: center;
          margin-bottom: 30rpx;
          i{
            display: inline-block;
            font-size: 30rpx;
            color:#fff;
            margin-left:16rpx;
          }
        }
      }
    }

  }
</style>
