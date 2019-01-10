<template>
  <div class="dwzn">
    <scroll-view :scroll-y="true" class="scroll">
      <Infolist :list="list"></Infolist>
    </scroll-view>
  </div>
</template>

<script>

  import Infolist from '../../base/infoList/infoList'
  import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        list:[]
      }
    },
    methods:{
      initlist(){
        var that=this;
        wx.request({
          url: conf.HOST+"/cloud-app/servlet/dynamic.action?method=getDynamicByChannel",
          data: {
            CHANNEL_ID:8,
            pageIndex:1,
            pageSize:10
          },
          header: {
            'content-type': 'application/json' // 默认值
          },
          success (res) {

            that.list=res.data;
            // console.log(that.list)

          }
        });
      }
    },

    onLoad () {
      this.initlist();
      console.log(0)
    },

    components: {
      Infolist
    },
  }
</script>

<style scoped lang="less">
  .dwzn{
    width: 100%;
    height: 100vh;
    .scroll{
      width: 100%;
      height: 100vh;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
    }
  }
</style>
