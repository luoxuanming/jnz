<template>
  <div class="login">
      <div class="head">
        <img src="../../images/login_bg.jpg" mode="widthFix" class="login_bg" alt="">
        <div class="logobox">
       
          <p>江南中街道党群服务中心</p>
        </div>
      </div><!--背景+logo END-->
      <div class="body">
        <div class="form_bg">
          <dl>
           
            <dd><input type="text" v-model="username" placeholder="请输入真实姓名，提交后不可修改"></dd>
          </dl>
        </div>
        <div class="form_bg">
          <dl>
           
            <dd>
              <picker @change="bindPickerChange0" :value="index0" :range="array0">
                <view class="picker">
                    {{array0[index0]?array0[index0]:array0[0]}} 
                    <i class="iconfont icon-xiala"></i>
                </view>
              </picker>
            </dd>
          </dl>
        </div>
        <div class="form_bg">
          <dl>
           
            <dd>
              <picker @change="bindPickerChange" :value="index" :range="array">
                <view style=" text-align: left;" class="picker"> {{array[index]?array[index]:'请选择所属党支部'}} <i class="iconfont icon-xiala"></i></view>
              </picker>
            </dd>
          </dl>
        </div>
        <div class="form_bg">
          <dl>
           
            <dd><input type="text" v-model="tel" placeholder="请输入11位手机号"></dd>
          </dl>
        </div>
        
        <!--<div class="form_bg last">-->
          <!--<dl>-->
            <!--<dt>验证码</dt>-->
            <!--<dd><span class="yzm">发送验证码</span></dd>-->
          <!--</dl>-->
        <!--</div>-->

        <img style="width: 586rpx;height: 113rpx;margin-top: 50rpx;" @click="login" src="../../images/loginBtn.png"/>
       
      </div><!--表单验证END-->
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        index:"",
        index0:"",
        array:[],
        array0:['江南中街道','地区单位'],
        orgIdList:[],
        username:"",
        tel:"",
        orgId:-1,
        userInfo:''
      }
    },

    created () {
        var that=this;
          wx.getStorage({
            key: 'userInfo',
            success(res) {
              that.userInfo=res.data
            }
          })
    },
    methods:{
      login(){
        var that=this;
        if(this.username){
          if(this.tel){
            if(!(/^1[34578]\d{9}$/.test(this.tel))){
              wx.showToast({
                title: '手机号码有误，请重填',
                icon: 'none',
                duration: 2000
              })
            }else{
              if(this.orgId==-1){
                wx.showToast({
                  title: '请选择党支部',
                  icon: 'none',
                  duration: 2000
                })
              }else{
                wx.showToast({
                  title: '登录中',
                  icon: 'loading',
                  duration: 20000
                })
                wx.getStorage({
                  key: 'userInfo',
                  success (ret) {
                      wx.request({
                            url:`${conf.HOST}/eac-tvmodule/servlet/miniWx?method=MiniWxlogin`,
                            data:{
                              openId:that.userInfo.openid,
                              userName:that.username,
                              userMobile:that.tel,
                              orgId:that.orgId,
                              userPic:that.userInfo.avatarUrl
                            },
                            success(res){
                              console.log(JSON.stringify(res))
                              if(res.data.success==false){
                                wx.showToast({
                                  title: '登录失败',
                                  icon: 'none',
                                  duration: 2000
                                })
                              }else{
                                
                                wx.getStorage({
                                  key: 'userInfo',
                                  success(response) {
                                    console.log(JSON.stringify(res.data));
                                    var userInfo=response.data;
                                    userInfo.USER_ID=res.data.USER_ID;
                                    userInfo.USER_CODE=res.data.USER_CODE;
                                    userInfo.ORG_ID=res.data.ORG_ID;
                                    wx.setStorage({
                                      key: 'userInfo',
                                      data:userInfo
                                    });
                                    wx.hideToast()
                                    wx.reLaunch({
                                      //跳转首页
                                      url:`/pages/index/main`
                                    });
                                  }
                                })
                              }
                            }
                          });
                  }
                })

              }
            }
          }else{
            wx.showToast({
              title: '请输入手机号',
              icon: 'none',
              duration: 2000
            })
          }
        }else{
          wx.showToast({
            title: '请输入姓名',
            icon: 'none',
            duration: 2000
          })
        }

      },
      getOrg(type){
        //获取组织列表
        var that=this;
        wx.getStorage({
          key: 'token',
          success (ret) {
            wx.request({
              url:`${conf.HOST}/eac-tvmodule/servlet/miniWx?method=getOrgan`,
              data:{
                      type:type
              },
              header: {
                'content-type': 'application/json', // 默认值
                'Authorization':ret.data.token
              },
              success(res){
                console.log(res)
               
                  that.array=res.data.orgNameList;
                  that.orgIdList=res.data.orgIdList;
                
              }
            })
          }
        })

      },
      bindPickerChange(e){
        this.index=e.target.value;
        this.orgId=this.orgIdList[e.target.value];
      },
      bindPickerChange0(e){
        
        this.index0=e.target.value;
        if(e.target.value==0){
          this.getOrg(2);
        }else{
          this.getOrg(1);
        }
        
        //this.orgId=this.orgIdList[e.target.value];
      }
    },
    onShow(){
      this.getOrg(2);
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  .login{
    width: 100%;
    height: 100vh;
    overflow: hidden;

      .head{
        position: relative;
        margin-bottom: 20rpx;
        .login_bg{
          width: 100%;
        }
        .logobox{
          width: 100%;
          margin-bottom: 15rpx;
          text-align: center;
          .logo{
            width: 96rpx;
            margin-bottom:10rpx;
          }
          p{
           font:500 35rpx "微软雅黑";
            color:#e82c2c;
            margin-bottom:45rpx;
              margin-top:-70rpx;


          }
        }
      }
      .body{
        width: 100%;
        padding:0 80rpx;
        box-sizing: border-box;
        .form_bg{
          width:100%;
          height:100rpx;
          border-bottom:1rpx solid #ededed;

          dl{
            width: 100%;
            height:100rpx;
            display: flex;
            align-items: center;
            font:26rpx "微软雅黑";
            dt{
              width: 178rpx;
              padding-left:28rpx;
              box-sizing: border-box;
              color:#333333;
              float: left;
            }
            dd{
              flex:1;
              width: 100%;
              text-align: left;
              color:#a0a1a5;
              padding-right:28rpx;
              box-sizing: border-box;
              overflow: hidden;
              span{
                color:#4a86ff;
              }
              input{
                width: 100%;
              }
              .picker{
                display: flex;
                align-items: center;
                justify-content:flex-end;
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
                i{
                  font-size: 26rpx;
                  color:#a0a1a5;
                  margin-left: 10rpx;
                  justify-content:flex-end;
                  display:flex;
                  float:right;
                  flex:1;

                }
              }
            }
          }
        }
        .last{
          margin-bottom: 82rpx;
        }
        .login_btn{
          width: 100%;
          height: 88rpx;
          background:#e82c2c;
          color:#fff;
          text-align: center;
          border-radius: 10rpx;
          font:36rpx "微软雅黑";
          line-height: 88rpx;
          margin-top:20px;

        }
      }

  }
</style>
