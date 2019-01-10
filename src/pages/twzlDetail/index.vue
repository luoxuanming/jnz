<template>
  <div class="twzl">
    <scroll-view :scroll-y="true">
      <div class="twzl_container">
        <h3>{{title}}</h3>
        <div class="text">
          <wxParse :content="article" :imageProp="imgmode" />
        </div>
      </div>
    </scroll-view>
  </div>
</template>

<script>
  import wxParse from 'mpvue-wxparse'
  import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        title:"",
        article:"",
        imgmode:{
          mode:"widthFix",
          domain:conf.IP
        },
      }
    },
    methods:{
      getTwzlResDetail(userId,resId){
        var that=this;
        wx.request({
          url:`${conf.HOST}/stddj-gzgj/servlet/twzl.action?method=getTwzlResDetail`,
          data:{
            resId:resId,
            userId:userId
          },
          success(res){
            console.log(JSON.stringify(res.data.RES_NAME));
            that.title=res.data.RES_NAME;
            var html0 =res.data.RES_CONTENT;
            var html1 = html0.replace(/\s+style="[^"]*"/g,'')
            var newHtml = html1.replace(/<img/g, '<img style="max-width:100%;border-radius:10rpx;"')
            that.article=`<div style="font-size:30rpx !important;">${newHtml}</div>`;
          }
        })
      }
    },
    created () {

    },
    onLoad(params){
      var userId=params.userId;
      var resId=params.resId;
      console.log(userId+":"+resId);
      this.getTwzlResDetail(userId,resId);
    },
    components: {
      wxParse
    },
  }
</script>

<style scoped lang="less">
  @import url("~mpvue-wxparse/src/wxParse.css");
  @import "../../common/css/less/base";
  .twzl{
    width: 100%;
    .twzl_container{
      width: 100%;
      padding:20rpx 30rpx;
      box-sizing: border-box;
    }
    h3{
      font:30rpx "微软雅黑";
      line-height: 50rpx;
      color:#333;
      font-weight: 600;
      text-align: center;
      padding-bottom: 20rpx;
      border-bottom: 1rpx solid #f2f2f2;
    }
    .text{
      font:30rpx "微软雅黑";
      color:#333;
    }
  }
</style>
