<template>
  <div class="answering">
    <scroll-view class="scroll" :scroll-y="true">
      <div class="state">
        <div class="content">
          <div class="circle">
            <i class="iconfont icon-gou"></i>
            <dl>
              <dt>心声已提交</dt>
              <dd>{{detail.HANDLE_TIME}}</dd>
            </dl>
          </div>
          <div class="default_line"></div>
          <div class="circle" v-if="detail.COMMENT_STATUS=='未回复'">
            <i class="iconfont icon-loudou"></i>
            <dl>
              <dt>未回复</dt>
              <dd>请耐心等待</dd>
            </dl>
          </div>
          <div class="circle" v-if="detail.COMMENT_STATUS=='已回复'">
            <i class="iconfont icon-gou"></i>
            <dl>
              <dt>已回复</dt>
              <dd>{{detail.HANDLE_TIME}}</dd>
            </dl>
          </div>
        </div>
      </div>
      <div class="xq">
        <div class="content2">
          <h4>心声详情</h4>
          <div class="text" :class="flag?'brief_more':' '">
            <p>{{detail.COMMENT_NOTES}}</p>
            <div class="more" @click="toMore" :class="flag?'gd_none':' '">查看更多 <i class="iconfont icon-xiala"></i></div>
            <div class="borderline" :class="flag?'gd_none':' '"><div></div></div>
          </div>
        </div>
      </div>
      <div class="hf" v-if="detail.COMMENT_RESULT">
        <div class="content">
          <h4>回复详情</h4>
          <div class="list">
            <div class="head">
              <img v-if="detail.USER_PIC==null" src="../../images/user_pic.png" alt="">
              <img v-else :src="detail.USER_PIC" alt="">
              <dl>
                <dt>{{detail.HADLE_USER_NAME}}</dt>
                <dd>{{detail.HANDLE_TIME}}</dd>
              </dl>
            </div>
            <div class="article">
              <p>{{detail.COMMENT_RESULT}}</p>
            </div>
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
        flag:false,
        detail:{}
      }
    },

    created () {

    },
    onLoad(params){
      this.getCommentDetail(params.comId);
    },
    methods:{
      toMore(){
        this.flag=true;
      },
      getCommentDetail(commentId){
        var that=this;
        wx.request({
          url:`${conf.HOST}/stddj-gzgj/servlet/comment.action?method=getCommentDetail`,
          data:{
            commentId
          },
          success(res){
            console.log(JSON.stringify(res.data))
            that.detail=res.data;
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
  .answering{
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
      .state{
        background: #fff;
        width: 100%;
        height: 190rpx;
        .circle{
          display: flex;
          .iconfont{
            font-size: 96rpx;
            color:#79ceff;
            margin-right: 24rpx;
          }
          .icon-loudou{
            color:#7f8699;
          }
          dl{
            display: flex;
            flex-direction: column;
           justify-content: center;
            dt{
              font:30rpx "微软雅黑";
              color:#333;
              margin-bottom: 10rpx;
            }
            dd{
              font:22rpx "微软雅黑";
              color:@smfontColor;
            }
          }
        }
        .line{
          width: 88rpx;
          height: 2rpx;
          background:#79ceff;
        }
        .default_line{
          width: 88rpx;
          height: 2rpx;
          background:#7f8699;
        }
        >.content{
          display: flex;
          justify-content: space-between;
          align-items: center;
        }
      }
      .xq{
        background: #fbfdfe;
        padding-top:14rpx;
        .text{
          width: 100%;
          height: 230rpx;
          overflow: hidden;
          position: relative;
          padding:0 40rpx;
          box-sizing: border-box;
          font:32rpx "微软雅黑";
          line-height:50rpx;
          color:#333;
          text-align: justify;
          padding-bottom: 30rpx;
          img{
            width: 100%;
          }
          .more{
            width: 100%;
            height: 146rpx;
            background:
              linear-gradient(to bottom,
              rgba(255,255,255,0),
              rgba(255,255,255,0.8),
              rgba(255,255,255,1),
              rgba(255,255,255,1),
              rgba(255,255,255,1));
            position: absolute;
            bottom: 0;
            left: 0;
            font:24rpx "黑体";
            line-height:164rpx;
            text-align: center;
            color:#79ceff;
            display: flex;
            justify-content: center;
            iconfont{
              font-size: 12rpx;
              color:#79ceff;
            }
          }
          .gd_none{
            display: none;
          }
          .borderline{
            width: 100%;
            height: 2rpx;
            padding: 0 40rpx;
            box-sizing: border-box;
            position: absolute;
            bottom: 0;
            left: 0;
            div{
              width: 100%;
              height: 100%;
              background: #cccccc;
            }
          }
        }
        .brief_more{
          height: auto;
        }
      }
      .hf{
        width: 100%;
        padding:14rpx 0;
        background: #fff;
        box-sizing: border-box;
        h4{
          margin-bottom: 30rpx;
        }
        .list{
          .head{
            width: 100%;
            display: flex;
            align-items: center;
            margin-bottom: 10rpx;
            img{
              width: 80rpx;
              height: 80rpx;
              border-radius: 40rpx;
              margin-right: 28rpx;
            }
            dl{
              dt{
                font:30rpx "微软雅黑";
                color:#333;
                margin-bottom: 10rpx;
              }
              dd{
                font:22rpx "黑体";
                color: #7f8699;
              }
            }
          }
          .article{
            font:30rpx "微软雅黑";
            color:#333;
            line-height: 50rpx;
            text-align: justify;
          }
        }
      }
      h4{
        height:88rpx;
        font:38rpx "黑体";
        font-weight:bold;
        line-height:88rpx;
        letter-spacing:-2rpx;
      }
      .content{
        width: 100%;
        padding:0 40rpx;
        box-sizing: border-box;
      }
      .content2{
        h4{
          padding-left: 40rpx;
        }
      }
    }

  }
</style>
