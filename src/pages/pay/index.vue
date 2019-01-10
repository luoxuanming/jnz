<template>
  <div class="dfjn">
    <scroll-view class="scroll" :scroll-y="true">
      <div class="msg content">
        请核缴费信息，待缴金额可修改至少更高
      </div>
      <div class="content">
        <div class="card">
          <dl>
            <dt>
              党员姓名
            </dt>
            <dd>
              赵广军
            </dd>
          </dl>
          <dl>
            <dt>
              所在支部
            </dt>
            <dd>
              江南中党支部
            </dd>
          </dl><dl>
          <dt>
            缴费月份
          </dt>
          <dd>
            2019-12
          </dd>
        </dl>
          <dl>
            <dt>
              代缴金额（元）
            </dt>
            <dd>
              0.01
            </dd>
          </dl>
        </div>
      </div>
      <div class="content">
        <div class="btn">
          确认缴纳
        </div>
      </div>
    </scroll-view>
  </div>
</template>

<script>

  export default {

    data () {
      return {
        placeholder:"差党建服务站、搜重点单位",
        cardlist:[1,2],
        pastlist:[1,2]
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
  .dfjn{
    .scroll{

    }
    .content{
      width: 100%;
      padding:0 30rpx;
      box-sizing: border-box;
    }
    .msg{
      font:28rpx "微软雅黑";
      color:#333;
      padding-top:20rpx;
      margin-bottom:20rpx;
    }
    .card{
      width: 100%;
      box-shadow: 0 0 6rpx #e0e0e0;
      border-radius: 20rpx;
      background: #fff;
      overflow: hidden;
      box-sizing: border-box;
      margin-bottom: 100rpx;
      dl{
        width: 100%;
        padding:30rpx;
        box-sizing: border-box;
        border-bottom: 1rpx solid #ededed;
        display: flex;
        justify-content: space-between;
        font: 30rpx "微软雅黑";
        color:#333;
        dt{

        }
        dd{
          color:#999999;
        }
      }
      dl:last-child{
        flex-direction: column;
        dd{
          padding:70rpx 0;
          text-align: center;
          font:100rpx "微软雅黑";
          color:#000;
          word-spacing:8rpx;
          letter-spacing: 0rpx;
        }
      }
    }
    .btn{
      width: 100%;
      height: 80rpx;
      background: @mainColor;
      color:#fff;
      font:30rpx "微软雅黑";
      line-height: 80rpx;
      border-radius:10rpx;
      text-align: center;

    }
  }

</style>
