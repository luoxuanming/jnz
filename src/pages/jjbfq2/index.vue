<template>
  <div class="jjb">
    <scroll-view :scroll-y="true" class="scroll">
      <div class="state">
        <div class="content">
          <div class="circle">
            <i class="iconfont icon-gou active"></i>
            <dl>
              <dt>已完成</dt>
              <dd>选择发起类型</dd>
            </dl>
          </div>
          <div class="default_line"></div>
          <div class="circle">
            <i class="iconfont icon-loudou active"></i>
            <dl>
              <dt>进行中</dt>
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

      <div class="info">
        <div class="content">
          <h4>填写信息</h4>
          
          <dl class="list">
            <dt>
              开始时间<span class="xing">*</span>
            </dt>
            <dd>
              <span class="picker" :class="startTime==''?'moren':' '" @click="handleTime(0)">{{startTime==''?'请选择':startTime}} <i class="iconfont icon-xiala"></i></span>
            </dd>
          </dl>
          <dl class="list">
            <dt>
              结束时间<span class="xing">*</span>
            </dt>
            <dd>
              <span class="picker" :class="endTime==''?'moren':' '" @click="handleTime(1)">{{endTime==''?'请选择':endTime}} <i class="iconfont icon-xiala"></i></span>
            </dd>
          </dl>
          <dl class="list">
            <dt>
              地点<span class="xing">*</span>
            </dt>
            <dd>
              <input style="text-align:right;" v-model="address" type="text" placeholder="请输入不超过50字的地址">
            </dd>
          </dl>
          <dl class="list">
            <dt>
              参与人
            </dt>
            <dd>
              <picker @change="bindPickerChange3" :value="index3" :range="array3">
                <view class="picker" :class="index3==0?'moren':' '">
                  {{array3[index3]}} <i class="iconfont icon-xiala"></i>
                </view>
              </picker>
            </dd>
          </dl>
        
          <dl class="list zt" style="height: 240rpx !important">
            <dt>
              主题 <span class="xing">*</span>
            </dt>
            <dd style="width: 100%;">
              <textarea v-model="theme"  type="text" style="width: 100%;height: 160rpx;font-size: 30rpx;" placeholder="输入此次相聚的主题，限制200字内"/>
            </dd>
          </dl>
        </div>
      </div>
     
      
      
      <div class="btn_groups content" style="background:#fff">
   
        <div class="btns">
          <div @click="preStep">上一步</div>
          <div @click="fabu">发布 <i class="iconfont icon-fabu"></i> </div>
          <!--<div>发布 <i class="iconfont icon-fabu"></i> </div>-->
        </div>
      </div>
      <hljPickerMpvue :visible="mpFlag" :value="mpArr" :otherOptions="otherArr" @confirm="confirm" :showYearsRange="6" @close="close"></hljPickerMpvue>
    </scroll-view>
  </div>
</template>

<script>
  //import dateTimePicker from '../../utils/index'
  import * as conf from '../../utils/config'
  import hljPickerMpvue from "hlj-picker-mpvue"
  export default {

    data () {
      return {
        mpArr:[],//默认选中当前时间
        otherArr:[],
        mpFlag:false,
        startTime:"",
        endTime:"",
        timeType:0,
        date: '2018-10-01',
        time: '12:00',
        dateTimeArray: null,
        dateTime: null,
        dateTimeArray1: null,
        dateTime1: null,
        startYear: 2000,
        endYear: 2050,
        address:'',//地点
        theme:'',//主题
        typeText:'',
        start1:"2015-01-01",
        end1:"2020-09-01",
        date1:"请选择",
        index3:0,
        array3:[
          "不限制"
        ]
      }
    },
   
    methods:{
      fabu(){
       
       if(this.startTime==''){
            
             wx.showToast({
              title: '请选择开始时间',
              icon: 'none',
              duration: 20000
            })
            return false;
        }else if(this.endTime==''){
          wx.showToast({
              title: '请选择结束时间',
              icon: 'none',
              duration: 2000
            })
            return false;
        }else if(this.address==''){
            wx.showToast({
              title: '请输入地址',
              icon: 'none',
              duration: 2000
            })
            return false;
        }else if(this.theme==''){
            wx.showToast({
              title: '请输入主题',
            icon: 'none',
              duration: 2000
            })
            return false;
        }else{
          /*
          console.log(this.startTime)
          console.log(this.endTime)
          console.log(this.address)
          console.log(this.theme)
          console.log(this.typeText)
       */
          var that =this;
            wx.request({
              url:`${conf.HOST}/stddj-jjb/servlet/meeting.action?method=addMeeting`, 
              data: {
                userId: that.userInfos.USER_ID,
                meetingTitle: that.theme,
                meetingType:that.typeText,
                beginTime:that.startTime,
                endTime:that.endTime,
                meetingAddr:that.address,
                attendOrgId:1
                //meetingTopic:that.theme
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success(res) {
              console.log(res)
                if(res.data.success){
                  wx.showModal({
                      title: '提示',
                      content: '发起成功，是否回到聚聚吧首页',
                      success(res) {
                        if (res.confirm) {
                          wx.navigateBack({
                              delta: 2
                            })
                        } else if (res.cancel) {
                          console.log('用户点击取消')
                          
                        }
                      }
                    })
                }else{
                  wx.showToast({
                    title: '发布失败',
                     icon: 'none',
                    duration: 2000
                  })
                  return false;
                }
              }
            })
           
        }
        
      },
      bindDateChange(e){
        // console.log(e.target.value)
        this.date=e.target.value;
      },
      handleTime(index){
        if(index=='0'||index==0){
          this.timeType=0;
        }else{
          this.timeType=1;
        }
        this.mpFlag=true;
      },
      confirm(e){
        let dateArr=e.slice(0,3);
        let timeArr=e.slice(3);

        let date=dateArr.join('-');
        let time=timeArr.join(':');
        let value=date+" "+time;
        //console.log(that.timeType);
        if(this.timeType==0){
          //开始时间
         this.startTime=value;
        }else{
          //结束时间
          this.endTime=value;
          //console.log(value)
        }
        this.mpFlag=false;//关闭picker
      },
      bindDateChange1(e){
        //console.log(e.target.value)
        this.date1=e.target.value;
      },
      bindPickerChange3(e){
        // console.log(e.target.value)
        this.index3=e.target.value;
      },
      preStep(){
        wx.navigateBack({
          delta:1
        })
      },
      getHourMinArr(){
        var arrmin=[];
        var arrsec=[];
        for(var i=0;i<24;i++){
          var value=i;
          if(i<10){
            value='0'+i;
          }
          arrmin.push(parseInt(value))
        }
        for(var i=0;i<60;i++){
          var value=i;
          if(i<10){
            value='0'+i;
          }
          arrsec.push(parseInt(value))
        }
        this.otherArr[0]=arrmin;
        this.otherArr[1]=arrsec;
      },
      initCurrentTime(){
        var d=new Date();
        var year=d.getFullYear();
        var month=d.getMonth()+1;
        var date=d.getDate();
        var hour=d.getHours();
        var min=d.getMinutes();
        this.mpArr=[year,month,date,hour,min];
      }
    },
    onLoad(option) {
     
      this.typeText=option.type;
    },
    created(){
      this.getHourMinArr();//获取时分数组
      this.initCurrentTime();//获取当前时间
       var that=this;
      wx.getStorage({
            key: 'userInfos',
            success(res) {
              that.userInfos=res.data
            }
          })
    },
    components: {
      hljPickerMpvue
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

        }
        .icon-xiala{
          margin-left: 12rpx;
          font-size: 26rpx;
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
      background: #f6f8fd;
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
