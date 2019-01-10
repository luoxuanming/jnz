<template>
    <div>
      <div class="list" @click="goNewsDetail(item.NEWS_ID)"  v-for="(item,index) in list" :key="index">
        <dl>
          <dt>{{item.ALIAS_TITLE}}</dt>
          <dd>
            <span>{{item.MODIFY_TIME}}</span>
            <span class="count">{{item.READ_COUNT}} 阅读</span>
          </dd>
        </dl>
        <img v-if="item.NEWS_THUMB_IMG!=null" :src="item.NEWS_THUMB_IMG" @error="errorfn(index)" alt="">
      </div>
      <!--<div class="list" @click="goNewsDetail()" v-for="(item,index) in list" :key="index">-->
        <!--<dl>-->
          <!--<dt>深圳开发开发40年深圳开发开发40年深圳开发开发40年深圳开发开发40年深圳开发开发40年</dt>-->
          <!--<dd>-->
            <!--<span>2018/09/15 17:00</span>-->
            <!--<span class="count">2323 阅读</span>-->
          <!--</dd>-->
        <!--</dl>-->

      <!--</div>-->
    </div>
</template>

<script>
    export default {
      data () {
        return {
          imgerror:'111'
        }
      },
      props:{
        list:{
          type:Array,
          require:true
        }
      },
      updated(){

      },
      methods:{
        goNewsDetail(id){
          wx.navigateTo({
            url:`/pages/newsDetail/main?newsId=`+id
          });
        },
        errorfn(index){
          this.list[index].NEWS_THUMB_IMG="../../images/default_img.jpg"
        }
      }

      // watch: {
      //   list: {
      //     handler: function (val, oldval) {
      //       this.$nextTick(function () {
      //         this.newlist = val;
      //       })
      //     },
      //     deep: true //对象内部的属性监听，也叫深度监听
      //   }
      // }
    }
</script>

<style scoped lang="less">
    .list{
      width:692rpx;
      margin:0 auto;
      display: flex;
      align-items:center;
      justify-content: space-between;
      height:178rpx;
      box-sizing:border-box;
      padding:24rpx 0;
      background: #fff;
      border-bottom: 1rpx solid #f2f2f2;
      overflow: hidden;
      dl{
        flex:1;
        box-sizing: border-box;
        overflow: hidden;
        dt{
          height: 85rpx;
          font:30rpx "微软雅黑";
          margin-bottom:10rpx;
          text-align: justify;
          overflow: hidden;
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
        height:128rpx;
        margin-left:80rpx;
        box-sizing: border-box;
      }
    }
</style>
