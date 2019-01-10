<template>
  <div class="twzlejfl">
    <div class="bottom">
      <scroll-view class="left" :scroll-y="true">
        <div class="flml" :class="current==0?'active':''">
          分类一级目录
        </div>
        <div class="flml">
          分类一级目录
        </div>
      </scroll-view>
      <scroll-view class="right" :scroll-y="true">
        <div class="flnr">
          <scroll-view class="pic_show" :scroll-x="true">
            <div class="pic_list">
              <img src="../../images/default_img.jpg" alt="">
              <p>习近平论全面从严治习近平论全面从严治</p>
            </div>
            <div class="pic_list">
              <img src="../../images/default_img.jpg" alt="">
              <p>习近平论全面从严治习近平论全面从严治</p>
            </div>
          </scroll-view>
          <div class="fl_block">
            <div class="title">
              <h3>分类二级目录</h3>
              <div class="more">
                查看更多 <span> > </span>
              </div>
            </div>
            <div class="twzl_list">
              <p>图文资料占位图文资料占位图文资料占位</p>
              <div>
                <span>总课程<span>4</span>节</span>
                <span>2018-12-27 20:19</span>
                <span>4学分</span>
              </div>
            </div>
            <div class="twzl_list">
              <p>图文资料占位图文资料占位图文资料占位</p>
              <div>
                <span>总课程<span>4</span>节</span>
                <span>2018-12-27 20:19</span>
                <span>4学分</span>
              </div>
            </div>
          </div>
          <div class="fl_block">
            <div class="title">
              <h3>分类二级目录</h3>
              <div class="more">
                查看更多 <span> > </span>
              </div>
            </div>
            <div class="twzl_list">
              <p>图文资料占位图文资料占位图文资料占位</p>
              <div>
                <span>总课程<span>4</span>节</span>
                <span>2018-12-27 20:19</span>
                <span>4学分</span>
              </div>
            </div>
            <div class="twzl_list">
              <p>图文资料占位图文资料占位图文资料占位</p>
              <div>
                <span>总课程<span>4</span>节</span>
                <span>2018-12-27 20:19</span>
                <span>4学分</span>
              </div>
            </div>
          </div>
        </div>
      </scroll-view>
    </div>
  </div>
</template>

<script>

  export default {

    data () {
      return {
        current:0
      }
    },

    created () {

    },
    components: {
    },
  }
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  .twzlejfl{
    .bottom{
      width: 100%;
      height: 100vh;
      display: flex;
      .left{
        width: 234rpx;
        background: #F3F6FD;
        height: 100%;
        overflow: hidden;
        .flml{
          width: 100%;
          height: 90rpx;
          background: #F3F6FD;
          color:#7F8699;
          border-left: 6rpx solid transparent;
          font:30rpx "微软雅黑";
          line-height: 90rpx;
          text-align: center;
          padding-right: 6rpx;
          box-sizing: border-box;
        }
        .active{
          background: #fff;
          color:@mainColor;
          border-color: @mainColor;
        }
      }
      .right{
        flex: 1;
        height: 100%;
        background: #fff;
        overflow: hidden;
        .flnr{
          padding-top:28rpx;
          padding-left: 24rpx;
          box-sizing: border-box;
          .pic_show{
            width: 100%;
            white-space: nowrap;
            overflow:hidden;
            margin-bottom: 60rpx;
            .pic_list{
              width: 310rpx;
              display: inline-block;
              margin-right: 24rpx;
              img{
                width: 100%;
                height: 185rpx;
                border-radius:10rpx;
                margin-bottom:10rpx;
              }
              p{
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
                font:30rpx "微软雅黑";
                color:#333;
              }
            }
          }
          .fl_block{
            margin-bottom: 60rpx;
          }
          .title{
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-right: 24rpx;
            margin-bottom: 20rpx;
            overflow: hidden;
            h3{
              font:600 32rpx "微软雅黑";
              color:#333;
            }
            .more{
              height: 100%;
              display: flex;
              font:22rpx "黑体";
              color:#7F8699;
              align-items: center;
              span{
                font:22rpx "宋体";
                margin-left: 5rpx;
              }
            }
          }
          .twzl_list{
            font:30rpx "微软雅黑";
            color:#333;
            padding:20rpx 0;
            margin-right: 24rpx;
            border-bottom: 1rpx solid #F2F2F2;
            margin-bottom: 10rpx;
            p{
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
              padding-right: 20rpx;
              margin-bottom: 30rpx;
            }
            div{
              display: flex;
              justify-content: space-between;
              align-items: center;
              span{
                font:22rpx "黑体";
                color:#7F8699;
                span{
                  color:#333;
                }
              }
              span:last-child{
                color:@mainColor;
              }
            }
          }

        }
      }
    }
  }
</style>
