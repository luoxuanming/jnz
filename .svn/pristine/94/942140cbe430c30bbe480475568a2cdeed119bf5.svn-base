<template>
  <div class="infoPublish">
   <scroll-view :scroll-y="true" class="scroll">
     <div class="list" @click="goNewsDetail()" v-for="(item,index) in list">
       <dl>
         <dt>深圳开发开发40年：“烂泥渡”摇变“最摩登”（专题文章标题</dt>
         <dd>
           <span>2018/09/15 17:00</span>
           <span class="count">2323 阅读</span>
         </dd>
       </dl>
       <img src="../../images/dy_pic01.png" alt="">
     </div>
   </scroll-view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list:[
        1,2,3,4,5,6,7
      ]
    }
  },
  created () {

  },
  methods:{
    goNewsDetail(){
      wx.navigateTo({
        url:`/pages/newsDetail/main`
      })
    }
  },
  components: {},

}
</script>

<style scoped lang="less">
  @import "../../common/css/less/base";
  .infoPublish{
    background: @bglow;
  }
  .scroll{
    width:100%;
    height: 100vh;
    padding-top:10rpx;
    box-sizing: border-box;
    overflow: hidden;
    .list{
      width:726rpx;
      margin:0 auto;
      display: flex;
      align-items:center;
      border-radius: 10rpx;
      justify-content: space-between;
      height:178rpx;
      box-sizing:border-box;
      padding:24rpx 0;
      background: #fff;
      padding:20rpx;
      overflow: hidden;
      margin-bottom: 10rpx;
      dl{
        width:490rpx;
        box-sizing: border-box;
        overflow: hidden;
        dt{
          font:30rpx "微软雅黑";
          margin-bottom:5rpx;
        }
        dd{
          span{
            font:24rpx "黑体";
            color:#7f8699;
          }
          .count{
            margin-left:36rpx;
          }
        }
      }
      img{
        width:198rpx;
        height:123rpx;

      }
    }
  }
</style>
