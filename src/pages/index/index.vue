<template>
  <div class="dj_container">
    <scroll-view  class="scroll" :scroll-y="true">
      <div class="login">
        <img src="http://139.159.180.215/resource/images/login.png" alt="" class="login_bg">
        <div class="user_info">
          <!--<img v-if="userInfos.avatarUrl" :src="userInfos.avatarUrl" :alt="userInfos.avatarUrl">-->
          <!--<img v-else src="../../images/user_pic.png">-->
          <!--<span class="username">{{userInfos.nickName}}</span>-->
          <div class="avatarbox" @click="goCenter">
            <open-data class="avatar" type="userAvatarUrl"></open-data>
          </div>

          <open-data class="username" type="userNickName"></open-data>
          <!--
          <span v-if="loginState">积分:30</span>
          -->
          <button v-if="loginState" style="margin-right:-60rpx;" open-type="getUserInfo" @click="goLogin" :plain="true" lang="zh_CN" >请登录</button>
          <button v-else style="margin-right:-60rpx;" open-type="getUserInfo" :plain="true" lang="zh_CN" >{{ORGNAME}}</button>
        </div>
        <div class="temperature">
          <img src="../../images/cloud.png" alt="">
          <span>20℃</span>
        </div>
      </div>
      <div class="wrap"><!--轮播图-->
        <swiper class="slider"
                @change="swiperChange"
                :indicator-dots="false"
                :circular="true"
                :autoplay="true"
                :current="swiperCurrent"
                :interval="2000"
                :duration="400">
          <block v-for="(item,index) in imgUrls" :key="index">
            <swiper-item style="position: relative;">
              <img :src="item.img" class="slide_image"/>
              <!--
              <p class="text">{{item.text}}</p>
              <img class="xuImg" src="../../images/xu.png" />
              -->
            </swiper-item>

          </block>
        </swiper>
        <!--重置小圆点的样式  -->
        <div class="dots">
          <block>
            <span  v-for="(item,index) in imgUrls" :key="index"  class="dot" :class="index==swiperCurrent?'active':' '"></span>
          </block>
        </div>
      </div>
      <Listbar></Listbar>
      <div class="hr"></div>
      <Linedzb></Linedzb><!--线上党支部-->
      <div class="hr"></div>
      <Tab :channellist="channellist"></Tab>
    </scroll-view>
    <div class="layer" v-if="false">
      <div class="qd_wrap">
        <div class="top">
          <img src="../../images/qd_bg.png" alt="">
          <dl>
            <dt class="iconfont icon-qiandao"></dt>
            <dd>签到成功</dd>
          </dl>
        </div>
        <div class="bottom">
          <dl>
            <dt>恭喜获得</dt>
            <dd>积分+10</dd>
          </dl>
          <div class="btn" @click="close">好的</div>
        </div>
      </div>
    </div>
    <div class="layer1" v-if="false">

    </div>
    <img src="http://139.159.180.215/resource/images/jf.gif" class="jf" alt="" mode="widthFix" @click="goJf">
  </div>
</template>

<script>
  import navgation from '../../base/navigation/navigation'
  import Login from '../../components/login/login'
  import Listbar from '../../components/listbar/listbar'
  import Linedzb from '../../components/linedzb/linedzb'
  import Tab from '../../base/tab/tab'
  import Infolist from '../../base/infoList/infoList'
  import {mapState,mapMutations,mapGetters} from "Vuex";
  import * as conf from '../../utils/config'
  export default {
    data () {
      return {
        channellist:[],//频道分类
        userInfos:{},//用户信息
        swiperCurrent:0,//当前轮播图的索引值
        imgUrls:[//轮播图片地址
          {img:'http://139.159.180.215/resource/images/server.png',text:'党建小程序上线啦！'},
           {img:'http://139.159.180.215/resource/images/server1.png',text:'打造共同体 共画同心圆'}

        ],
        userAccount:conf.userAccount,
        userPwd:conf.userPwd,
        getuserinfo:{},
        canIUse:false,
        loginState:false,
        openid:'',
        ORGNAME:'',
        show:true
      }
    },
    methods: {
      swiperChange: function (e) {
        // console.log(JSON.stringify(e.mp.detail.current));
        this.swiperCurrent=e.mp.detail.current;//获取当前轮播图的index值
      },
      login(){
         var that=this;
         wx.getStorage({
            key: 'openid',
            success(res) {
              that.openid=res.data
            }
          })
      },
      close(){
        this.show=false;
      },
      getUserInfo () {
        var that=this;
        wx.getSetting({
          // 查看是否授权
          success(ress) {
            // console.log(ress.authSetting['scope.userInfo'])
            that.canIUse=ress.authSetting['scope.userInfo'];
            if (ress.authSetting['scope.userInfo']) {
              // 已经授权，可以直接调用 getUserInfo 获取头像昵称

              var userInfo={}
              wx.login({
                success: (ret) => {
                  //console.log(conf.AppId+":"+conf.AppSecret+":"+ret.code)
                  //that.aa=conf.AppId+":"+conf.AppSecret+":"+ret.code;
                  wx.request({
                    //获取open-id
                    url:`${conf.HOST}/eac-tvmodule/servlet/miniWx?method=MiniWxloginApi&appid=${conf.AppId}&secret=${conf.AppSecret}&code=${ret.code}&grant_type=authorization_code`,
                    data:{},
                    header: {
                      'content-type': 'application/json' // 默认值
                    },
                    success(response){
                      console.log(response)
                      wx.setStorage({
                        key: 'openid',
                        data:response.data.openid
                      });
                      /*判断是否登录 */
                      wx.request({
                        //是否登录
                        url:`${conf.HOST}/eac-tvmodule/servlet/miniWx?method=MiniWxChecklogin`,
                        data:{
                          openId:response.data.openid
                        },
                        success(ret1){
                            if(ret1.data.success){
                              //绑定系统后台数据
                             // console.log(ret1)
                              wx.setStorage({
                                key: 'userInfos',
                                data:ret1.data.userInfo
                              });

                              //绑定token
                              wx.setStorage({
                                key: 'token',
                                data:ret1.data.token
                              });
                              that.loginState=false;
                              that.ORGNAME=ret1.data.userInfo.ORG_NAME
                          }else{
                            that.loginState=true;
                          }
                        }
                      })
                      /*判断是否登录 END*/
                      wx.getUserInfo({
                        success: (res) => {

                          // that.$nextTick(function(){
                            that.setUserInfos(res.userInfo);
                            userInfo=res.userInfo;

                            that.userInfos=res.userInfo;
                            //that.canIUse=JSON.stringify(res.userInfo.nickName);
                            userInfo.session_key=response.data.session_key;
                            userInfo.openid=response.data.openid;
                            wx.setStorage({
                              key: 'userInfo',
                              data:userInfo
                            });

                          // });
                        }
                      });
                      /*
                      wx.request({
                        //登录来获取token值
                        url: conf.HOST+"/cloud-app/servlet/login.action?method=login",
                        data: {
                          userAccount:that.userAccount,
                          userPwd:that.userPwd
                        },
                        header: {
                          'content-type': 'application/json' // 默认值
                        },
                        success (res) {
                          that.setToken(res.data.userInfo.token);
                          wx.setStorage({
                            key: 'token',
                            data:res.data.userInfo.token
                          });
                        }
                      });
                      */

                    }
                  });
                }
              });
            }
          },
          fail(re){

          }
        })

      },
      getchannle(){
        var that=this;
        wx.request({
          //获取频道分类
          url: conf.HOST+"/cloud-app/servlet/dynamic.action?method=getChannel",
          data: {
            orgId:1,
            CHANNEL_ID:1
          },
          header: {
            'content-type': 'application/json' // 默认值
          },
          success (res) {
            //console.log(JSON.stringify(res.data))
            that.$nextTick(function(){
              that.channellist=res.data;
            })
          }
        });
      },
      goJf(){
        wx.navigateTo({
          url:`/pages/outLink/main?type=5`
        })
      },
      goLogin(){
        var that=this;

        if(that.loginState){
          wx.navigateTo({
            url:`/pages/login/main`
          });
        }else{
          that.getUserInfo();
        }

      },
      goCenter(){
        wx.navigateTo({
          url:`/pages/myCenter/main`
        })
      },
      ...mapMutations({
        setUserInfos: 'SET_USERINFOS',
        setToken:'SET_TOKEN'
      })
    },
    created () {
      // 调用应用实例的方法获取全局数据
      this.getUserInfo();
      this.getchannle();
      //this.login()
    },
    onShow(){
      this.getUserInfo();
    },
    components: {
      Login,
      Listbar,
      Linedzb,
      Tab,
      navgation
    }

  }
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  @import "../../common/css/less/base";
  .dj_container{
    width:100%;
    height: 100vh;
    position: relative;
    box-sizing: border-box;
    overflow-x:hidden;
    padding-top:0;
    .layer{
      width:100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      padding:0 130rpx;
      box-sizing: border-box;
      position: absolute;
      left: 0;
      top:0;
      z-index: 999;
      .qd_wrap{
        width: 100%;
        height: 510rpx;
        background: #fff;
        -webkit-border-radius: 20rpx;
        -moz-border-radius: 20rpx;
        border-radius: 20rpx;
        .top{
          width: 100%;
          height: 236rpx;
          position: relative;
          dl{
            width: 100%;
            height: 236rpx;
            position: absolute;
            left: 0;
            top:0;
            color:#fff;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-items: center;
            padding-top:36rpx;
            box-sizing: border-box;
            dt{
              font-size: 78rpx;
              margin-bottom: 20rpx;
            }
            dd{
              font:40rpx "微软雅黑";
            }
          }
          img{
            width: 100%;
            height: 100%;
          }
        }
        .bottom{
          width: 100%;
          text-align: center;
          padding:40rpx 0;
          box-sizing: border-box;
          dl{
            color:#333;
            margin-bottom: 20rpx;
            dt{
              margin-bottom: 5rpx;
            }
            dd{}
          }
          .btn{
            width: 224rpx;
            height: 60rpx;
            font:32rpx "微软雅黑";
            line-height: 60rpx;
            color:#fff;
            text-align: center;
            margin:0 auto;
            background: @mainColor;
            -webkit-border-radius: 30rpx;
            -moz-border-radius: 30rpx;
            border-radius: 30rpx;
          }
        }
      }
    }
    .layer1{
      width:100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      position: absolute;
      top:0;
      left: 0;
      z-index: 999;
    }
    .scroll{
      width: 100%;
      height: 100vh;
      box-sizing: border-box;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
    }
    .wrap{
      position: relative;
      .slider{
        width:692rpx;
        height: 290rpx;
        background: #fff;
        border-radius: 10rpx;
        margin:12rpx auto 20rpx;
        overflow: hidden;
        .slide_image{
          width:100%;
          border-radius: 10rpx;
          height:290rpx;
        }
        p.text{
          position:absolute;
          bottom:0;
          width:100%;
          color:rgba(255,255,255,0.9);
          font:30rpx "黑体";
          margin-bottom:40rpx;
          padding-left:20rpx;
          z-index: 999;
        }
        img.xuImg{
          position:absolute;
          bottom:-150rpx;
          left: 0;
          width:100%;
        }
      }
      .dots{
        width: 156rpx;
        height: 20rpx;
        display: flex;
        flex-direction: row;
        position: absolute;
        left: 320rpx;
        bottom: 0rpx;
        .dot{
          width: 6rpx;
          height: 6rpx;
          border-radius:4rpx;
          margin-right: 14rpx;
          background-color: rgba(255, 255, 255, 0.3);
        }
        .active{
          width: 45rpx;
          height: 6rpx;
          border-radius: 8rpx;
          background-color: rgba(255,255,255,0.7);
        }
      }
    }
    .hr{
      width:100%;
      height:16rpx;
      background: #f3f6fd;
    }

  }
  .jf{
    width:148rpx;
    position:absolute;
    bottom:220rpx;
    right:0;
    z-index: 99;
  }
  /******/
  .login{
   // width:692rpx;
   width:100%;
    height:200rpx;
    background: #fff;
    margin:0 auto;
    position:relative;
    .login_bg{
      width:100%;
      height:210rpx;
      display:flex;
      position: relative;
      z-index: 10;
    }
    .user_info{
      position: absolute;
      width:692rpx;
      height:70rpx;
      bottom:0;
      left:0;
      display:flex;
      align-items:center;
      box-sizing:border-box;
      padding:0 26rpx;
      z-index: 10;
      padding-left:60rpx;

      img{
        width:68rpx;
        height:68rpx;
        border-radius:34rpx;
        box-shadow:2rpx 2rpx 3rpx rgba(221,221,221,0.7);
        position: relative;
        margin-top:-50rpx;
      }
      .avatarbox{
       width:75rpx;
        height:75rpx;
        border-radius:50%;
        box-shadow:2rpx 2rpx 3rpx rgba(221, 221, 221, 0.7);
        overflow:hidden;
        margin-top:-55rpx;


      }
      .avatar{
        width:68rpx;
        height:68rpx;
        border-radius:34rpx;
        box-shadow:2rpx 2rpx 3rpx rgba(221,221,221,0.7);
        position: relative;
        margin-top:-8rpx;
      }
      .username{
        font:30rpx "黑体";
        margin-left:16rpx;
      }
      span{
        margin-left: 10rpx;
        font:30rpx "黑体";
      }
      span:nth-of-type(2),button{
        font:28rpx "黑体";
        margin-left:22rpx;
        color:#7f8699;
      }
      button{
        position:absolute;
        right:26rpx;
        border:none
      }
    }
    .temperature{
      position: absolute;
      width:100%;
      height:22rpx;
      top:30rpx;
      left:0;
      padding-left:66rpx;
      z-index: 20;
      img{
        width:44rpx;
        height:32rpx;
        position:absolute;
        left:10rpx;
        top:0rpx;
        animation:cloud 2s linear infinite alternate;
      }
      span{
        font:24rpx "微软雅黑";
        color:#999999;
        position:absolute;
        left:65rpx;
        top:0rpx;
      }
    }
  }
  //温度云运动
  @keyframes cloud {
    0%{}
    100%{
      transform: translateX(10rpx);
    }
  }

</style>
