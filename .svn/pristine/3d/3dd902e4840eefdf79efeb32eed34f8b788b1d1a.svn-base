<template>
  <div class="volunteerAct">
    <div class="searchBox">
      <div class="search">
        <div class="addr"><i></i><span>江南中街道</span></div>
        <div class="input_area">
          <i></i>
          <input type="text" :placeholder="placeholder">
        </div>
      </div>
      <div class="content">
        <div class="btnGroups">
          <div class="btn">志愿者申请</div>
          <div class="btn">活动日历</div>
        </div>
      </div>
    </div>
    <div class="cards">
      <div class="content">
        <div class="cardlist" v-for="(item,index) in cardlist" >
          <div class="pic">
            <img src="../../images/pic01.png" alt="" class="banner">
            <span>进行中</span>
          </div>
          <div class="cont">
            <div><p>志愿活动名称占位志愿活动名称占位志...</p><i></i></div>
            <dl>
              <dt><i></i>广东广州天河去</dt>
              <dd><i></i>10.09 周六 10:00</dd>
            </dl>
          </div>
        </div>
      </div>
    </div><!--卡片END-->
    <div class="past">
      <div class="content">
        <div class="title">往期志愿活动</div>
        <div class="actlist" v-for="(item,index) in pastlist" :key="index">
         <div class="pic">
           <img src="../../images/dy_pic02.png" alt="">
           <span>进行中</span>
           <div class="text">关爱小动物</div>
         </div>
         <div class="info">
           <p>
             志愿活动名称占位志愿活动名称占位志...
           </p>
           <dl>
             <dt><i></i>广东广州天河区</dt>
             <dd><span><i></i>10.09 周六 10:00</span><span><i></i>志愿活动</span></dd>
           </dl>
         </div>
        </div>
      </div>
    </div><!--服务公告END-->
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
  .volunteerAct{
    width: 100%;
    .searchBox{
      display: flex;
      flex-direction: column;
      .search{
        width: 100%;
        height: 96rpx;
        background: #fff;
        padding:26rpx 20rpx;
        display: flex;
        align-items: center;
        justify-content: space-between;
        box-sizing: border-box;
        .addr{
          display: flex;
          align-items: center;
          color:#7f8699;
          i{}
          span{
            font:28rpx "黑体";
          }
        }
        .input_area{
          width: 508rpx;
          height: 60rpx;
          background:#f7f8fc;
          border-radius: 10rpx;
          padding-left: 70rpx;
          box-sizing: border-box;
          display: flex;
          align-items: center;
          input{
            width: 100%;
            font:28rpx "黑体";
            line-height:60rpx;
          }
          input::placeholder{
            color:#bfbfbf;
          }
        }
      }

        .btnGroups{
          width: 100%;
          display: flex;
          justify-content:space-around;
          padding-bottom: 26rpx;
          .btn{
            width: 326rpx;
            height:82rpx;
            border:1rpx solid #f2f2f2;
            border-radius: 10rpx;
            font:30rpx "微软雅黑";
            line-height: 82rpx;
            text-align: center;
            color:#4d5068;
          }
        }
      }
    .cards{
      background: #f6f8fd;
      padding:20rpx 0;
      .cardlist{
        width: 100%;
        height: 372rpx;
        border-radius:10rpx;
        margin-bottom: 20rpx;
        overflow: hidden;
        background: #fff;
        .pic{
          width: 100%;
          height: 226rpx;
          position: relative;
          .banner{
            width: 100%;
            height: 226rpx;
          }
          span{
            display: block;
            width: 100rpx;
            height: 40rpx;
            font:20rpx "黑体";
            line-height: 40rpx;
            background: #d40303;
            color:#fff;
            text-align: center;
            position: absolute;
            right: 24rpx;
            top:0;
            border-radius:0 0 10rpx 10rpx;
          }
        }
        .cont{
          padding:22rpx;
          box-sizing: border-box;
          >div{
            margin-bottom: 16rpx;
            p{
              width: 508rpx;
              height: 40rpx;
              line-height: 40rpx;
              font:30rpx "微软雅黑";
              color:#333;
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
            }
          }
          dl{
            font:20rpx "黑体";
            color:#7f8699;
            dt{}
            dd{}
          }
        }
      }
      .cardlist:last-child{
        margin-bottom: 0;
      }
    }
    .past{
      .actlist{
        display: flex;
        padding:0 20rpx;
        padding-bottom: 30rpx;
        margin-bottom: 30rpx;
        border-bottom:1rpx solid #f2f2f2;
        box-sizing: border-box;
        .pic{
          position: relative;
          width: 280rpx;
          height: 150rpx;
          border-radius:8rpx;
          margin-right: 26rpx;
          overflow: hidden;
          img{
            width: 280rpx;
            height: 150rpx;
          }
          span{
            display: block;
            width: 86rpx;
            height: 30rpx;
            font:22rpx "黑体";
            text-align: center;
            color:#fff;
            background: #d40303;
            border-radius:0 0 6rpx 6rpx;
            position: absolute;
            top:0;
            left: 16rpx;
          }
          .text{
            width: 100%;
            height: 30rpx;
            font:22rpx "黑体";
            background: rgba(0,0,0,0.5);
            color:#fff;
            text-align: center;
            position: absolute;
            left: 0;
            bottom: 0;
          }
        }
          .info{
            p{
              font:30rpx "黑体";
              color:#333;
              height: 80rpx;
              overflow: hidden;
              position: relative;
              margin-bottom: 12rpx;
            }
            dl{
              font:22rpx "黑体";
              color:#999999;
              dt{}
              dd{
                display: flex;
                span:first-child{
                  margin-right: 36rpx;
                }
              }
            }
          }
        }
      .title{
        width: 100%;
        font:32rpx "黑体";
        height:120rpx;
        line-height: 120rpx;
        font-weight: bold;
        color:#000;
        padding:0 20rpx;
        box-sizing: border-box;
      }
    }
    .content{
      width: 712rpx;
      margin:0 auto;
    }
  }
</style>
