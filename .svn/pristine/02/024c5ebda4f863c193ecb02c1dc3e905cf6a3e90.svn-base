<template>
  <div class="mapsearch">
    <div class="search">
      <Search :placeholder="placeholder"></Search>
    </div>
    <div class="content">
      <div class="hot">
        <h3>热门搜索</h3>
        <div class="hot_content">
          <div @click="goResult(1)">街道党群中心</div>
          <div @click="goResult(2)">社区党群服务站</div>
          <div @click="goResult(3)">重点单位</div>
          <div @click="goResult(4)">党支部</div>
          <div @click="goResult(5)">社区党委</div>
          <div @click="goResult(6)">街道党工委</div>
        </div>
      </div>
      <div class="recent" v-if="history.length">
        <h3>最近搜索</h3>
        <ul>
          <li v-for="(item,index) in history" :key="index" @click="goSearch(item)">
            <i class="iconfont icon-shijian"></i>
            {{item}}
          </li>
        </ul>
        <div class="clear" @click="clearHistory">清空历史搜索记录</div>
      </div>
    </div>
  </div>
</template>

<script>
import Search from '../../base/search/search'
import * as conf from "../../utils/config.js"
import {mapState,mapMutations,mapGetters} from "Vuex";
export default {
  data () {
    return {
      placeholder:"查党群服务站、搜重点单位",
      history:[],
      searchId:""
    }
  },

  onShow() {
    var that=this;
    wx.getStorage({
      key:"record",
      success(res){
        that.$nextTick(function(){
          that.history=res.data;
        })
      }
    });
  },
  methods:{
    goResult(id){
      let pages = getCurrentPages();
      let prevPage = pages[ pages.length - 2 ];
      prevPage.setData({  // 将我们想要传递的参数在这里直接setData。上个页面就会执行这里的操作。
        searchId:id
      });
      this.setboxflag(false);
      this.setfirstflag(true);
      this.settwoflag(true);
      wx.setStorage({
        key: 'type',
        data: id,
        success(){
          wx.navigateBack({
            delta: 1  // 返回上一级页面。
          })
        }
      });

    },
    goSearch(item){
      console.log(item)
      var that=this;
      wx.getStorage({
        key:`Location`,
          success(ret) {
            wx.request({
              url: `${conf.HOST}/stddj-gzgj/servlet/map.action?method=searchOrgan`,
              data: {
                lon: ret.data.lon,
                lat: ret.data.lat,
                context:item
              },
              success(res){
                if(res.data.length){
                  wx.setStorage({
                    key: 'mapSearch',
                    data:res.data,
                    success(response){
                      wx.navigateBack();
                      that.setboxflag(false);
                      that.setfirstflag(true);
                      that.settwoflag(true);
                    }
                  })
                }
              }
            })
          }
      })
    },
    clearHistory(){
      var that=this;
      wx.removeStorage({
        key: 'record',
        success(ret) {
          wx.showToast({
            title:"历史记录已清除",
            icon:"none",
            duration:2000
          })
          that.history=[];
        }
      })
    },
    ...mapMutations({
      setboxflag: 'SET_BOXFLAG',
      setfirstflag: 'SET_FIRSTFLAG',
      settwoflag: 'SET_TWOFLAG',
      setthreeflag: 'SET_THREEFLAG'
    })
  },
  components: {
    Search
  }
}
</script>

<style scoped lang="less">
  .mapsearch{
    .content{
      width: 692rpx;
      margin:0 auto;
      .search{
        margin-bottom:50rpx;
      }
      .hot,.recent{
        padding:26rpx 0;
        box-sizing: border-box;
        .hot_content{
          div{
            display: inline-block;
            padding:14rpx 12rpx;
            border:1rpx solid #d7dce9;
            color:#666666;
            border-radius: 10rpx;
            font:28rpx "黑体";
            box-sizing: border-box;
            margin:0 7rpx;
            margin-bottom: 14rpx;
          }
        }
        ul{
          padding:18rpx 20rpx;
          padding-top:0;
          li{
            display: flex;
            align-items: center;
            color:#333333;
            font:28rpx "黑体";
            height: 79rpx;
            line-height: 79rpx;
            border-bottom: 1rpx solid #f6f5fa;
            i{
              font-size: 22rpx;
              margin-right: 24rpx;
              color:#81889b;
              margin-left: 12rpx;
            }
          }

        }
        .clear{
          height: 79rpx;
          font:22rpx "黑体";
          line-height: 79rpx;
          text-align: center;
          color:#7f8699;
          border-bottom: none;
        }
      }
      h3{
        font:32rpx "黑体";
        font-weight: bold;
        margin-bottom: 34rpx;
      }
    }

  }

</style>
