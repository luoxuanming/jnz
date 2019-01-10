<template>
    <div class="linedzb">
      <div class="content">
        <h4>线上党支部</h4>
        <ul>
          <li @click="goDetail('/pages/jjb/main')">
            <dl>
              <dt>聚聚吧</dt>
              <dd>沟通零距离</dd>
            </dl>
            <img src="../../images/linedzb01.png" alt="">
          </li>
          <li @click="goDetail('/pages/dnfg/main')">
            <dl>
              <dt>党内法规</dt>
              <dd>学党章用党章</dd>
            </dl>
            <img src="../../images/linedzb02.png" alt="">
          </li>
          <li @click="goDetail('/pages/dwzn/main')">
            <dl>
              <dt>党务指南</dt>
              <dd>党务工作小助手</dd>
            </dl>
            <img src="../../images/linedzb03.png" alt="">
          </li>
          <li @click="goDetail('/pages/dfjn/main')">
            <dl>
              <dt>党费缴纳</dt>
              <dd>便捷又安全</dd>
            </dl>
            <img src="../../images/linedzb04.png" alt="">
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
    export default {
       data(){
         return{}
       },
      methods:{
        goDetail(url){
          wx.navigateTo({
            url
          })
        }
      }
    }
</script>

<style scoped lang="less">
  .linedzb{
    width: 100%;
    padding:30rpx 0;
    background: #fff;
    padding-top:10rpx;

    .content{
      width:692rpx;
      margin:0 auto;
      h4{
        height:86rpx;
        font:35rpx "黑体";
        font-weight: bold;
        line-height:86rpx;
        letter-spacing: -2rpx;
      }
      ul{
        overflow: hidden;
        li{
          width:308rpx;
          height:120rpx;
          display:flex;
          align-items:center;
          float:left;
          dl{
            width:186rpx;
            /*margin-right:84rpx;*/
            dt{
              font:30rpx "微软雅黑";
              letter-spacing: -2rpx;
              margin-bottom:10rpx;
            }
            dd{
              font:20rpx "黑体";
              color:#7f8699;
            }
          }
          img{
            width:108rpx;
            height:100rpx;
          }
        }
        li:nth-child(2n){
          margin-left:76rpx;
        }
      }
    }
  }
</style>
