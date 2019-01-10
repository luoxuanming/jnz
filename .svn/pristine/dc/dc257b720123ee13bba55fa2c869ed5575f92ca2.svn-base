<template>
  <div class="chat">
    <scroll-view class="scroll" :scroll-y="true" :scroll-top="length" @click="closeGn">
      <div class="content top">
        <div class="head">
          <div class="title">{{getContent.MEETING_TITLE}}</div>
          <div class="type">
            <span v-for="(type,index1) in getContent.MEETING_TYPE" :key="index1">{{type}}</span>
           
          </div>
          <dl>
            <dt><i class="iconfont icon-dangzhibu"></i></dt>
            <dd>
             {{getContent.ORG_NAME}}
            </dd>
          </dl>
          <dl>
            <dt><i class="iconfont icon-dingwei1"></i></dt>
            <dd>
              
               {{getContent.MEETING_ADDR}}
            </dd>
          </dl>
          <dl>
            <dt><i class="iconfont icon-shijian"></i></dt>
            <dd>
             {{getContent.BEGIN_TIME}} ~ {{getContent.END_TIME}}
            </dd>
          </dl>
        </div>
        <p style="font-size: 26rpx;text-align: center;padding-bottom: 25rpx;color: #fc7c7c;">主持人与发起人可长按内容置顶</p>
      </div>
      <div class="content body" v-if="topRecord!=''">
        <div class="msg" style="z-index:999; position:relative">
          <div class="userInfo">
            <img v-if="getContent.topRecord.USER_PIC==null" src="../../images/user_pic.png" alt="">
            <img v-else :src="getContent.topRecord.USER_PIC" alt="">
            <div class="username">{{getContent.topRecord.POST_USER_NAME}}</div>
            <div class="zd">置顶</div>
            <div class="time">2018-12-23 10:00</div>
          </div>
          <div class="gg" :class="ggFlag==true?'gg2':' '">
            {{getContent.topRecord.POST_CONTENT}}
            
            <div class="more" :class="ggFlag==true?'more2':' '" @click="MoreFn">
              {{more}} <i class="iconfont icon-xiala"></i>
            </div>
          </div>
        </div>
      </div>
      <div class="content message" :class="gnFlag==true?'message2':''">
        <!--
        <div class="msgtime">
          <div class="current_time">
            12:00
          </div>
        </div>
      -->
        <div class="other" v-for="(itemLits,index) in replyMsgList" :key="index"  @longtap="longTap(index)">
    
          <div class="avatar">
            <img v-if="itemLits.USER_PIC==null" src="../../images/user_pic.png" alt="">
            <img v-else :src="itemLits.USER_PIC" alt="">
          </div>
          <div class="reply_msg">
            <div class="username">{{itemLits.POST_USER_NAME}}</div>
            <div class="text">{{itemLits.POST_CONTENT}}</div>
          </div>
        </div>
        <div class="my" v-if="mySendList.length" v-for="(item,index) in mySendList" :key="index">
          <div class="text">{{item.text}}</div>
          <div class="avatar">
            <img src="../../images/user_pic.png" alt="">
          </div>
        </div>
      </div>
    </scroll-view>
    <img class="nullImg" src="../../images/ly_null.png" v-if="nullImg"/>
    <div class="sendMsg" :class="gnFlag==true?'gnFlag':' '">
      <div class="send">
       
        <div>
          <input  placeholder="请输入回复" type="text" confirm-type="send" v-model="sendMessage" @input="confirm($event)">
        </div>
        <span @click="Reply" style="font-size:30rpx;color:#666">回复</span>
        <!--
           <i class="iconfont icon-yuyin1"></i>
        <i class="iconfont icon-biaoqing"></i>
        <i class="iconfont icon-gengduo3" @click="gnFn"></i>
        <i class="iconfont icon-shoucang1"></i>
        -->
      </div>
      <img style="position: fixed;bottom: 90rpx;left: 50%;margin-left: -100px;width: 360rpx;height: 290rpx;" class="nullImg" src="../../images/ly_null.png" v-if="nullImg"/>
      <div class="gn">
        <dl>
          <dt><i class="iconfont icon-zhaopian2"></i></dt>
          <dd>照片</dd>
        </dl>
        <dl>
          <dt><i class="iconfont icon-zhaopian11"></i></dt>
          <dd>拍摄</dd>
        </dl>
        <dl>
          <dt><i class="iconfont icon-wenjian1"></i></dt>
          <dd>文件</dd>
        </dl>
        <dl>
          <dt><i class="iconfont icon-zhiding1"></i></dt>
          <dd>置顶公告</dd>
        </dl>
        <dl>
          <dt><i class="iconfont icon-toupiao2"></i></dt>
          <dd>投票评议</dd>
        </dl>
      </div>
    </div>
  </div>
</template>

<script>
import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        gnFlag:false,
        ggFlag:false,
        more:"查看更多",
        sendMessage:"",
        mySendList:[],
        inputText:'',
        length:"",
         nullImg:false,
         getContent:'',
        id:'',
        replyMsgList:[],
        nowTotalRecordNum:0,
        userInfos:'',
        longTapOn:false,
        longTapList:'',
        token:''
      }
    },
    onLoad(option) {
       
        this.id=option.id
       
       this.getList(option.id);
        this.getContentX(option.id)
        var that=this;
       
      },
    created () {
     
   var that=this;
      wx.getStorage({
            key: 'userInfos',
            success(res) {
              that.userInfos=res.data
            }
          })
      wx.getStorage({
            key: 'token',
            success(res) {
              that.token=res.data
            }
          })
    },
    
    methods:{
      longTap: function(e) {
        var that=this;
       wx.showModal({
          title: '提示',
          content: '是否置顶该内容',
          success(res) {
            if (res.confirm) {
              console.log(that.replyMsgList[e].POST_CONTENT)
              wx.request({
              url:`${conf.HOST}/stddj-jjb/servlet/meeting.action?method=addMeetingPost`, // 仅为示例，并非真实的接口地址
              data: {
                userId:that.replyMsgList[e].POST_USER_ID,
                postContent:that.replyMsgList[e].POST_CONTENT,
                meetingId:that.id,
                isTop:1
              },
              header: {
                'content-type': 'application/json;charset=UTF-8',
                'Authorization':that.token
              },
              success(res) {
                console.log(res)
                if(res.data.success){
                    wx.showToast({
                      title: '置顶成功',
                    icon: 'none',
                      duration: 2000
                    })
                    that.longTapOn=true
                    that.getContentX(that.id);
                }else{
                   wx.showToast({
                      title: '置顶失败，请重试',
                    icon: 'none',
                      duration: 2000
                    })
                    that.longTapOn=false
                }
              }
            })
            } else if (res.cancel) {
              console.log('用户点击取消')
            }
          }
        })
        
      },
      gnFn(){
        this.gnFlag=!this.gnFlag;
      },
      closeGn(){
        this.gnFlag=false;
      },
      MoreFn(){
        //查看更多
        this.ggFlag=!this.ggFlag;
        if(this.ggFlag==false){
          this.more="查看更多"
        }else{
          this.more="收起"
        }
      },
      confirm(e){
        //console.log(e.target.value)
        this.inputText=e.target.value
        /*
        this.mySendList.push({
          text:e.target.value
        });
        this.length+=90;
        this.sendMessage="";
        */
      },
      Reply(){
        var that=this;
      
        if(that.inputText==''){
          console.log(that.id)
        }else{
          
           wx.request({
              url:`${conf.HOST}/stddj-jjb/servlet/meeting.action?method=addMeetingPost`, // 仅为示例，并非真实的接口地址
              data: {
                userId: that.userInfos.USER_ID,
                postContent:that.inputText,
                meetingId:that.id
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success(res) {
                that.getList(that.id);
             
                 that.sendMessage="";
              }
            })
        }
      },
      getList(id){
       var that=this;
     //  console.log(id+'----')
        wx.getStorage({
          key: 'token',
          success(ret) {
            wx.request({
              url:`${conf.HOST}/stddj-jjb/servlet/meeting.action?method=loadAllMeetingPostRecord`, // 仅为示例，并非真实的接口地址
              data: {
                MEETING_ID: id,
                nowTotalRecordNum: that.nowTotalRecordNum
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success(res) {
               console.log(res)
                if(res.data.success){
                  that.nullImg=false
                  
                  that.replyMsgList=res.data.data
                }else{
                  that.replyMsgList=''
                  that.nullImg=true
                }
                //that.replyMsgList.push([{"USER_PIC":null,"POST_ID":1,"POST_TYPE":1,"POST_CONTENT":"aaaaaa","POST_TIME":{"date":22,"day":6,"hours":14,"minutes":51,"month":11,"nanos":0,"seconds":52,"time":1545461512000,"timezoneOffset":-480,"year":118},"POST_USER_ID":0,"MEETING_ID":1,"RECORD_TIME":null,"POST_USER_NAME":"系统管理员"}]);
                
                //that.nowTotalRecordNum=res.data.data.length;
              }
            })
          }
        })

      },
      getContentX(id){
       var that=this;
  
        wx.getStorage({
          key: 'token',
          success(ret) {
            wx.request({
              url:`${conf.HOST}/stddj-jjb/servlet/meeting.action?method=getMeetingById`, // 仅为示例，并非真实的接口地址
              data: {
                meetingId: id,
              
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success(res) {
                console.log(res.data.info)
                that.getContent=res.data.info
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
  @import "../../common/css/font/iconfont.css";
.chat{
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
    box-sizing: border-box;
    background: #f6f8fd;
  }
  .content{
    width: 100%;
    padding:0 30rpx;
    box-sizing: border-box;
  }
  .head{
    width: 100%;
    background: #fff;
    padding:30rpx 24rpx;
    box-sizing: border-box;
    background: #fff;
    .title{
      font:30rpx "微软雅黑";
      color:#333;
      text-overflow: -o-ellipsis-lastline;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      line-clamp: 2;
      -webkit-box-orient: vertical;
      text-align: justify;
    }
    .type{
      width: 100%;
      margin-bottom: 30rpx;
      span{
        padding:6rpx 16rpx;
        background: #f3f6fd;
        font:22rpx "黑体";
        color:#fc7c7c;
        text-align: center;
        border-radius: 10rpx;
        margin-right: 12rpx;
      }
    }
    dl{
      display: flex;
      margin-bottom: 10rpx;
      dt{
        margin-right: 12rpx;
        i{
          font-size: 26rpx;
          color:#7f8699;
        }
        .icon-dingwei1{
          font-size: 28rpx;
          margin:0 -12rpx;
        }
      }
      dd{
        font:22rpx "黑体";
        color:#7f8699;
      }
    }
  }
  .top{
    background: #fff;
    margin-bottom:20rpx;
  }
  .body{
    width: 100%;
    background: #f6f8fd;
    box-sizing: border-box;
    .msg{
      width: 100%;
      padding:25rpx 30rpx;
      box-sizing: border-box;
      background: #fff;
      border-radius: 10rpx;
      margin-bottom: 10rpx;
      
      .userInfo{
        width: 100%;
        display: flex;
        align-items: center;
        img{
          width: 64rpx;
          height: 64rpx;
          border-radius: 32rpx;
          box-shadow:2rpx 2rpx 3rpx rgba(221,221,221,0.7);
        }
        .username{
          font:30rpx "微软雅黑";
          color:#333;
          margin:0 12rpx;
        }
        .zd{
          padding:2rpx 6rpx;
          border:1rpx solid #fc7c7c;
          border-radius:5rpx;
          font:22rpx "黑体";
          color:#fc7c7c;
          margin-right: 12rpx;
        }
        .time{
          font:22rpx "黑体";
          color:#7f8699;
        }
      }
      .gg{
        width: 100%;
        padding-left: 80rpx;
        padding-bottom: 80rpx;
        box-sizing: border-box;
        text-overflow: -o-ellipsis-lastline;
        overflow: hidden;
        display: -webkit-box;
        -webkit-line-clamp:3;
        -webkit-box-orient: vertical;
        font:30rpx "微软雅黑";
        line-height: 50rpx;
        color:#333;
        text-align: justify;
        position: relative;
        .more{
          position: absolute;
          left: 0;
          bottom: 0;
          width: 100%;
          height: 170rpx;
          background: linear-gradient(to bottom,
          rgba(255,255,255,0.2),
          rgba(255,255,255,0.8),
          rgba(255,255,255,1),
          rgba(255,255,255,1));
          text-align: center;
          font:24rpx "黑体";
          line-height: 272rpx;
          color:#7f8699;
          display: flex;
          justify-content: center;
          i{
            display: block;
            font-size: 24rpx;
            color:#7f8699;
            margin-left: 5rpx;
          }
        }
        .more2{
          background: transparent;
          i{
            display: none;
            color:transparent !important;
          }
        }
      }
      .gg2{
        -webkit-line-clamp:default !important;
        display:block !important;
      }
    }
  }
  .message{
    padding-bottom: 92rpx;
  }
  .message2{
    padding-bottom: 552rpx !important;
  }
  .my{
    width: 100%;
    display: flex;
    justify-content: flex-end;
    align-items: flex-start;
    margin-bottom: 30rpx;
    .text{
      position: relative;
      background: #fff;
      max-width: 490rpx;
      border-radius:10rpx;
      padding:10rpx 20rpx;
      box-sizing: border-box;
      margin-right: 20rpx;
      font:30rpx "微软雅黑";
      color:#333;
      text-align: justify;
    }
    .text::before{
      content:'';
      position: absolute;
      top:20rpx;
      right: -20rpx;
      width: 0;
      height: 0;
      border:10rpx solid #fff;
      border-color: transparent transparent transparent  #fff;
    }
  }
  .other{
    display: flex;
    justify-content: flex-start;
    margin-bottom: 50rpx;
    .username{
      font:22rpx "黑体";
      color:#333;
      padding-left: 22rpx;
      margin-bottom: 10rpx;
    }
    .text{
      position: relative;
      background: #fff;
      max-width: 490rpx;
      border-radius:10rpx;
      padding:10rpx 20rpx;
      box-sizing: border-box;
      margin-left: 20rpx;
      font:30rpx "微软雅黑";
      color:#333;
      text-align: justify;
    }
    .text::before{
      content:'';
      position: absolute;
      top:20rpx;
      left: -20rpx;
      width: 0;
      height: 0;
      border:10rpx solid #fff;
      border-color: transparent  #fff transparent transparent;
    }
  }
  .avatar{
    img{
      width: 64rpx;
      height: 64rpx;
      border-radius: 10rpx;
      box-shadow:2rpx 2rpx 3rpx rgba(221,221,221,0.7);
    }
  }
  .msgtime{
    width: 100%;
    height: 150rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    .current_time{
      width: 92rpx;
      height: 40rpx;
      border-radius:10rpx;
      background: #d7dce9;
      text-align: center;
      font:22rpx "黑体";
      line-height: 40rpx;
      color:#fff;
    }
  }
  .sendMsg{
    width: 100%;
    background: #fff;
    position: fixed;
    bottom:-460rpx;
    left: 0;
    z-index: 99;
    transition: all 0.3s;
    .send{
      width: 100%;
      height: 92rpx;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom:1rpx solid #d7dce9;
      padding:0 30rpx;
      box-sizing: border-box;
      i{
        font-size:56rpx;
        color:#7f8699;
      }
      div{
        width: 580rpx;
        height: 62rpx;
        border:1rpx solid #d7dce9;
        border-radius: 10rpx;
      }
      input{
        width: 100%;
        height:66rpx;
        padding-left:10rpx;
        font-size:30rpx;




      }
    }
    .gn{
      width: 100%;
      height: 460rpx;
      padding:42rpx 58rpx;
      padding-bottom: 0;
      box-sizing: border-box;
      display: flex;
      flex-wrap: wrap;
      background: #fff;
      dl{
        margin-right: 47rpx;
        margin-bottom: 46rpx;
        dt{
          width: 120rpx;
          height: 120rpx;
          border:1rpx solid #7f8699;
          border-radius: 10rpx;
          display: flex;
          justify-content: center;
          align-items: center;
          margin-bottom: 10rpx;
          i{
            font-size: 60rpx;
            color:#7f8699;
          }
        }
        dd{
          text-align: center;
          font:26rpx "微软雅黑";
          color:#7f8699;
        }

      }
      dl:nth-child(4){
        margin-right:0;
      }
    }
  }
  .gnFlag{
    bottom: 0 !important;
  }
}
</style>
