<template>
  <div class="lyform">
    <scroll-view class="scroll" :scroll-y="true">
      <div class="content">
        <div class="head">
          <img src="../../images/wzywkl.png" mode="widthFix" alt="">
        </div>
        <div class="text_area">
          <dl>
            <dt>
              姓名
              <span>*</span>
            </dt>
            <dd><input type="text" v-model="username" placeholder="请填写真实姓名"></dd>
          </dl>
          <dl>
            <dt>
              手机
              <span>*</span>
            </dt>
            <dd><input type="text" v-model="tel" placeholder="请填写手机号"></dd>
          </dl>
          <dl>
            <dt>
              工作单位
            </dt>
            <dd><input type="text" v-model="org" placeholder="请填写工作单位"></dd>
          </dl>
          <dl class="server_time">
            <dt>
              可服务时间
            </dt>
            <div>
              <dd>
                <picker @change="bindPickerChange" :value="index" :range="array">
                  <view class="picker" :class="index!=0?'active':''"> {{index==0?'请选择':arrstr}} <i class="iconfont icon-xiala"></i> </view>
                </picker>
              </dd>
              <dd>
                <picker @change="bindPickerChange1" :value="index1" :range="array1">
                  <view class="picker" :class="index1!=0?'active':''"> {{index1==0?'请选择':array1[index1]}} <i class="iconfont icon-xiala"></i> </view>
                </picker>
              </dd>
            </div>
          </dl>
          <dl class="comm">
            <dt>
              爱好特长
            </dt>
            <dd>
              <textarea name="" id="" v-model="content" placeholder="在此输入特长爱好，限制在200字内" class="textinput"></textarea>
            </dd>
          </dl>
        </div>
        <!--<div class="fj">-->
          <!--<div>-->
            <!--<img src="../../images/fj.png" class="fj" alt="">-->
            <!--添加附件-->
          <!--</div>-->
          <!--<div class="icon">+</div>-->
        <!--</div>-->
        <!--<div class="fj">-->
          <!--<div>-->
            <!--<img src="../../images/tp.png" class="fj" alt="">-->
            <!--添加图片-->
          <!--</div>-->
          <!--<div class="icon">+</div>-->
        <!--</div>-->
        <!--<div class="fj gk">-->
          <!--<div>是否公开</div>-->
          <!--<div class="icon"><switch checked @change="switch1Change" :color="color" class="wx-switch-input"/></div>-->
        <!--</div>-->
      </div>
      <div class="cys">
        <checkbox-group @change="checkboxChange">
        <label class="checkbox" >
          <checkbox :value="readed" :checked="readed"/>
          我已阅读
        </label><span @click="layerFn">《倡议书》</span>
        </checkbox-group>
      </div>
      <div class="btn">
        <div class="tj" @click="tj">申请加入</div>
      </div>
    </scroll-view>
    <div class="layer" v-show="cysLayer">
      <scroll-view class="scroll_layer" scroll-y="true">
        <div class="text">
          <h3>党员志愿服务——义卖献爱心活动倡议书</h3>
          亲爱的社区党员朋友：<br/>
          <p style="text-indent:2em">随着生活条件的改善，许多人家里都有大量闲置而有用的物品。而在我们的身边，也还有许多的生活困难人士。为此，我们计划组织社区党员开展义卖献爱心活动。</p>
          <p style="text-indent:2em">您可以捐赠或义卖家中闲置可用的物品，也可以自行创作工艺品进行义卖。我们将对您捐赠或义卖的物品进行逐一登记，并在活动当天公开义卖。本次义卖所得的收入全部用于帮助社区困难人员（具体款项用途将在社区公开，接受群众监督）。</p>
          <span style="font-weight: 600">参加义卖物品的要求：</span>品种不限，物品必须完整、可以正常使用<br/>
          <span style="font-weight: 600">义卖活动时间:</span>2015年6月6日上午9：00—11:30<br/>
          <span style="font-weight: 600">义卖活动地点:</span>万国广场门前广场（前进路侧）<br/>
          <p style="text-indent: 2em">
            一滴水也许是微不足道的，但如果汇成一股清泉就足以滋润干渴的心田。热切期盼您的积极参与，献出您的爱心，伸出您的援助之手。党员志愿服务活动因您的参与而更精彩！
          </p>
          <br/><br/>
          <p style="text-align: right;">江南中街道党员志愿服务中队</p>
          <p style="text-align: right;">2015年5月27日</p>
        </div>
        <div class="cys">
          <checkbox-group @change="checkboxChange" style="display: flex;">
          <label class="checkbox">
            <checkbox :value="readed" :checked="readed" @click="readedFn"/>
            我已阅读此
          </label>
          <span>《倡议书》</span> <p style="text-decoration: underline;" @click="close">关闭</p>
          </checkbox-group>
        </div>
      </scroll-view>
    </div>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'
  var arr=[];
  var arr2=[];
  export default {

    data () {
      return {
        index:0,
        index1:0,
        arrstr:[],
        array:[
          "请选择",
          "周一",
          "周二",
          "周三",
          "周四",
          "周五",
          "周六",
          "周日",
        ],
        array1:[
          "请选择",
          "上午",
          "下午",
          "全日"
        ],
        color:"#97abf4",
        username:"",
        tel:"",
        org:"",
        content:"",
        isShow:true,
        readed:false,
        cysLayer:false
      }
    },
    created () {

    },
    methods:{
      bindPickerChange(e){
        // console.log(e.target.value)
        this.index=e.target.value;
        if(this.index==0){
          return;
        }
        arr.push(this.array[this.index]);
        for(var i=0;i<arr.length;i++){
          if(arr2.indexOf(arr[i])==-1){
            arr2.push(arr[i]);
          }
        }
        this.arrstr=arr2.join(',');
        //console.log(JSON.stringify(arr2));
      },
      bindPickerChange1(e){
        // console.log(e.target.value)
        this.index1=e.target.value;

      },
      tj(){
        var that=this;
        //提交申请
        if(this.username){
          if(!(/^1[34578]\d{9}$/.test(this.tel))){
            wx.showToast({
              title: '手机号码有误，请重填',
              icon: 'none',
              duration: 2000
            })
          }else{
            if(this.readed){
              wx.getStorage({
                key: 'userInfos',
                success(ret) {
                  console.log(JSON.stringify(ret.data.USER_ID))
                  wx.request({
                    url:`${conf.HOST}/eac-tvmodule/RegistUser.action?method=registUser`,
                    data:{
                      USER_ID:ret.data.USER_ID,
                      USER_NAME:that.username,
                      USER_MOBILE:that.tel,
                      WORK_UNIT:that.org,
                      VOLUNTEER_DAY:that.arrstr,
                      VOLUNTEER_TIME:that.array1[that.index1],
                      SPECIALTY:""
                    },
                    header: {
                      'content-type': 'application/json' // 默认值
                    },
                    success(res){
                      //console.log(JSON.stringify(res.statusCode));
                      if(res.statusCode==200){
                        wx.showToast({
                          title: '该用户已注册志愿者，请耐心等待审核',
                          icon: 'none',
                          duration: 2000
                        })
                      }else{
                        wx.showToast({
                          title: '服务器出错了',
                          icon: 'loading',
                          duration: 2000
                        })
                      }
                    }
                  })
                },
                fail(){
                  wx.showToast({
                    title: '请登录后重试',
                    icon: 'none',
                    duration: 2000
                  })
                }
              })
            }else{
              wx.showToast({
                title: '请阅读倡议书后并勾选',
                icon: 'none',
                duration: 2000
              })
            }
          }
        }else{
          wx.showToast({
            title: '请填写姓名',
            icon: 'none',
            duration: 2000
          });
        }
      },
      checkboxChange(e){
        this.readed=!this.readed;
        //console.log(this.readed)
        //console.log(e.target.value)
      },
      layerFn(){
        this.cysLayer=true;
      },
      close(){
        this.cysLayer=false;
      }
    },
    onUnload(){
      this.cysLayer=false;
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  @import "../../common/css/font/iconfont.css";
  .lyform{
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
      .head{
        padding:0 30rpx;
        img{
          border-radius: 10rpx;
          width: 100%;
          margin-bottom: 20rpx
        }
      }
      .content{
        width: 100%;
        background: #fff;
        margin-bottom: 90rpx;
        .text_area{
          width: 100%;
          background: #fff;
          padding:0 40rpx;
          box-sizing: border-box;
          margin-bottom: 20rpx;
          dl{
            width: 100%;
            height: 80rpx;
            overflow: hidden;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1rpx solid #e4e4e4;
            dt{
              width: 200rpx;
              font:30rpx "微软雅黑";
              color:#333;
              span{
                color:@mainColor;
              }
            }
            dd{
              width: 100%;
              font:30rpx "微软雅黑";
              color:#999;
              overflow: hidden;
              text-align: right;
              .picker{
                display: flex;
                justify-content: flex-end;
                align-items: center;
                i{
                  font-size: 26rpx;
                  margin-left: 10rpx;
                  color:#999;
                }
              }
              .active{
                color:#333;
                i{
                  color:#333;
                }
              }
            }

          }
          .comm{
            display: flex;
            flex-direction: column;
            align-items: normal;
            height: auto;
            border: none;
            dt{
              display: flex;
              align-items: center;
              line-height: 80rpx;
              span{
                margin-left: 10rpx;
              }
            }
            dd{
              text-align: left;
              textarea{
                width: 100%;
                color:#333;
              }
              .textinput::-webkit-input-placeholder{
                color:#999;
              }
            }
          }
          .server_time{
            display: flex;
            align-items: flex-start;
            padding:20rpx 0;
            dd{
              margin-bottom: 5rpx;
            }
          }
        }

        .fj{
          width: 100%;
          height: 80rpx;
          display: flex;
          align-items: center;
          justify-content: space-between;
          background: #fff;
          margin-bottom: 20rpx;
          div{
            font:30rpx "微软雅黑";
            color:#333;
            padding:0 40rpx;
            height: 80rpx;
            display: flex;
            align-items: center;
            display: flex;
            align-items: center;
            img{
              width: 50rpx;
              height: 50rpx;
              margin-top:20rpx;
              margin-right: 20rpx;
            }
          }
          .icon{
            color:#d7dce9;
            font-size: 66rpx;
          }
        }
        .gk{
          margin-bottom: 0;
        }

      }
      .btn{
        width: 100%;
        padding:0 40rpx;
        box-sizing: border-box;
        position: fixed;
        bottom: 20rpx;
        left: 0;
        .tj{
          width: 100%;
          height: 86rpx;
          background: #97abf4;
          box-sizing: border-box;
          border-radius: 10rpx;
          text-align: center;
          font:30rpx "微软雅黑";
          color:#fff;
          line-height: 86rpx;
        }
      }
      .cys{
        width: 100%;
        padding:0 40rpx;
        box-sizing: border-box;
        position: fixed;
        bottom: 120rpx;
        left: 0;
        display: flex;
        align-items: center;
        font:30rpx "微软雅黑";
        span{
          color:#97abf4;
        }
      }
    }
    .layer{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      position: fixed;
      top:0;
      left: 0;
      background: rgba(255,255,255,1);
      z-index:99;
      .scroll_layer{
        width: 100%;
        height: 100%;
        overflow: hidden;
        box-sizing: border-box;
      }
      .cys{
        display: flex;
      }
      .icon-guanbi{
        position: fixed;
        right: 30rpx;
        bottom: 100rpx;
        font-size: 30rpx;
      }
      h3{
        font:38rpx "微软雅黑";
        color:#333;
        text-align: left;
        margin-bottom: 30rpx;
      }
      .text{
        font:30rpx "微软雅黑";
        color:#333;
        line-height: 50rpx;
        text-align: justify;
        margin:0 30rpx;
        margin-bottom: 100rpx;
      }
      .cys{
        width: 100%;
        margin:0 30rpx;
        margin-bottom: 100rpx;
        box-sizing: border-box;
        display: flex;
        align-items: center;
        font:30rpx "微软雅黑";
        line-height: 50rpx;
        .checkbox{
          display: flex;
          align-items: center;
        }
        span{
          color:#97abf4;
        }
      }
    }
  }
</style>
