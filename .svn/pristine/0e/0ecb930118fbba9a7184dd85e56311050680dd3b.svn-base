<template>
  <div class="search">
    <div class="input_area">
      <i class="iconfont icon-sousuo1"></i>
      <input type="text" :placeholder="placeholder"  @input="confirm($event)">
    </div>
    <span @click="Back">取消</span>
  </div>
</template>

<script>
  import * as conf from "../../utils/config"
  import {mapState,mapMutations,mapGetters} from "Vuex";
    export default {
       data(){
         return{
           search:"",
           record:[]
         }
       },
      methods:{
        Back(){
          wx.navigateBack();
        },
        confirm(e){
          //console.log(e.target.value);//input输入的内容
          var that=this;
          if(e.target.value){
            wx.getStorage({
              key:`Location`,
              success(ret){
                wx.request({
                  url:`${conf.HOST}/stddj-gzgj/servlet/map.action?method=searchOrgan`,
                  data:{
                    lon:ret.data.lon,
                    lat:ret.data.lat,
                    context:e.target.value
                  },
                  success(res){
                    if(res.data.length){
                      wx.setStorage({
                        key: 'mapSearch',
                        data:res.data,
                        success(response){
                          that.record.push(e.target.value);
                          var arr=[];
                          for(var i=0;i<that.record.length;i++){
                            if(arr.indexOf(that.record[i])==-1){
                              arr.push(that.record[i]);
                            }else{

                            }
                          }
                          wx.setStorage({
                            key:"record",
                            data:arr,
                            success(){
                              wx.navigateBack();
                              that.setboxflag(false);
                              that.setfirstflag(true);
                              that.settwoflag(true);
                            }
                          });
                        }
                      });
                    }else{
                      wx.showToast({
                        title:"未搜索到相关数据",
                        icon:"none",
                        duration:2000
                      })
                    }
                  }
                })
              }
            })
          }else{
            wx.showToast({
              title:"请输入查询信息",
              icon:"none",
              duration:2000
            })
          }

        },
        ...mapMutations({
          setboxflag: 'SET_BOXFLAG',
          setfirstflag: 'SET_FIRSTFLAG',
          settwoflag: 'SET_TWOFLAG',
          setthreeflag: 'SET_THREEFLAG'
        })
      },
      onLoad(){
        var that=this;
        wx.getStorage({
          key:"record",
          success(res){
            that.record=res.data;
          }
        })
      },
      props:{
        placeholder:{
          type:String,
          required:true
        }
      }
    }
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  .search{
    width: 100%;
    height: 96rpx;
    background: #fff;
    padding:26rpx 20rpx;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-sizing: border-box;
    .input_area{
      width: 600rpx;
      height: 60rpx;
      background:#f7f8fc;
      border-radius: 10rpx;
      padding-left: 70rpx;
      box-sizing: border-box;
      display: flex;
      align-items: center;
      position: relative;
      input{
        width: 100%;
        font:28rpx "黑体";
        line-height:60rpx;
      }
      input::placeholder{
        color:#bfbfbf;
      }
      .iconfont{
        position: absolute;
        left: 10rpx;
        font-size: 32rpx;
        color:#bfbfbf;
      }
    }
    span{
      font:28rpx "黑体";
      color:#bfbfbf;
      padding-right:14rpx;
      line-height:60rpx;
    }
  }
</style>
