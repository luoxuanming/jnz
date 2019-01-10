<template>
  <div class="djmap">
    <map
    id="myMap"
    style="width: 100%; height: 100vh;"
    :longitude="longitude"
    :latitude="latitude"
    :markers="markers"
    :show-location="true"
    :scale='12'
    subkey="WHQBZ-VMOKJ-A2CFI-KQHIA-GGAV3-4HBKV"
    :enable-rotate="true"
    @markertap="bindmarkertap"
    class="map"
    >
      <cover-view class="search">
        <cover-view class="input_area" @click="goMapSearch">
          <cover-image class="iconfont" src="../../images/sousou.png" />
          <cover-view class="text">查党群服务站、搜重点单位</cover-view>
        </cover-view>
        <cover-view class="cancel">取消</cover-view>
      </cover-view>

      <cover-view class="search_box" :class="boxflaghide">

        <cover-view class="content" :class="firsthide">
          <cover-view class="title">
            身边的党组织
            <cover-image src="../../images/close.png" class="iconfont" @click="closeBox"></cover-image>
            <cover-view class="borderB"></cover-view>
          </cover-view>
          <cover-view class="scroll sbzj">
            <cover-view class="resultlist" @click="goResult(1)">街道党群中心</cover-view>
            <cover-view class="resultlist" @click="goResult(2)">社区党群服务站</cover-view>
            <cover-view class="resultlist" @click="goResult(3)">重点单位</cover-view>
            <cover-view class="resultlist" @click="goResult(4)">党支部</cover-view>
            <cover-view class="resultlist" @click="goResult(5)">社区党总支</cover-view>
            <cover-view class="resultlist" @click="goResult(6)">街道党工委</cover-view>
          </cover-view>
        </cover-view>

        <cover-view class="content" :class="twohide">
          <cover-view class="title">
            距离您最近的
            <cover-view class="back" @click="toBeforeone">返回 <cover-image src="../../images/back.png" class="iconfont"></cover-image></cover-view>
            <cover-view class="borderB"></cover-view>
          </cover-view>
          <cover-view class="scroll">
            <cover-view class="jllist" v-for="(item,index) in jllist" :key="index">
              <cover-image class="disimg" :src="item.IMG" v-if="item.IMG!=null"></cover-image>
              <cover-view class="center"  @click="goSelect(item.ORG_ID)">
                <cover-view class="name">{{item.ORG_NAME}}</cover-view>
                <cover-view>
                  <cover-view class="addr">{{item.DISTANCE}}km <span v-if="item.ADDR">| {{item.ADDR==null?'':item.ADDR}}</span></cover-view>
                  <cover-view class="tel" v-if="item.ORG_TEL">联系电话:{{item.ORG_TEL}}</cover-view>
                </cover-view>
              </cover-view>
              <cover-view class="phone">
                <cover-image src="../../images/phone.png" class="icon" v-if="item.ORG_TEL" @click="Call(item.ORG_TEL)"></cover-image>
              </cover-view>
              <cover-view class="borderB"></cover-view>
            </cover-view>
          </cover-view>
        </cover-view>

        <cover-view class="content" :class="threehide" v-if="detail">
          <cover-view class="title">
            您选择了
            <cover-view class="back" @click="toBeforetwo">返回 <cover-image src="../../images/back.png" class="iconfont"></cover-image></cover-view>
            <cover-view class="borderB"></cover-view>
          </cover-view>
          <cover-view class="scroll">
          <cover-view class="jllist">
            <cover-image class="disimg" v-if="detail.IMG" :src="detail.IMG"></cover-image>
            <cover-view class="center" @click="goMore(detail.ORG_ID)">
              <cover-view class="name">{{detail.ORG_NAME}}</cover-view>
              <cover-view>
                <cover-view class="addr">{{detail.DISTANCE}}km <span v-if="detail.ADDR!=null">| {{detail.ADDR}}</span></cover-view>
                <cover-view class="tel">联系电话:{{detail.ORG_TEL}}</cover-view>
              </cover-view>
            </cover-view>
            <cover-view class="phone">
              <cover-image src="../../images/phone.png" class="icon" @click="Call(detail.ORG_TEL)"></cover-image>
            </cover-view>
            <cover-view class="borderB"></cover-view>
          </cover-view>

          <cover-view class="pingjia" v-if="detail.CONTENT">
            <cover-view class="jianjie">简介</cover-view>
            <cover-view class="textBox">
              <cover-view class="text">
                <wxParse  v-if="article" :content="article" :imageProp="imgmode" />
                </cover-view>
              <cover-image class="guodu" src="../../images/guodu.png" @click="goMore(detail.ORG_ID)"></cover-image>
            </cover-view>
          </cover-view>
          </cover-view>
        </cover-view>
      </cover-view>
    </map>
  </div>
</template>

<script>
  import {mapState,mapMutations,mapGetters} from "Vuex";
  import * as conf from "../../utils/config.js"
  import wxParse from 'mpvue-wxparse';
export default {

  data () {
    return {
      placehodler:"查党群服务站、搜重点单位",
      longitude:"113.26436",
      latitude:"23.12908",
      markers: [
        {
          iconPath: "/images/marker.png",
          id: 0,
          longitude: 113.26436,
          latitude: 23.12908,
          width: 30,
          height: 38,
          callout:{
            content:"江南中党总支部",
            bgColor:'#ffffff',
            padding:6,
            borderColor:"#ffffff",
            borderRadius:5
          }
        },
        {
          iconPath: "/images/marker.png",
          id: 1,
          longitude: 113.32436,
          latitude: 23.16908,
          width: 30,
          height:38,
          callout:{
            content:"江南中党总支部",
            bgColor:'#ffffff',
            padding:6,
            borderColor:"#ffffff",
            borderRadius:5
          }
        }
      ],
      polyline: [{
        points: [{
          longitude: 113.36199,
          latitude: 23.12463
        }, {
          longitude: 113.32436,
          latitude: 23.16908
        },{
          longitude: 113.26436,
          latitude: 23.12908
        }],
        color:"#039be5",
        width: 2,
        dottedLine: false
      }],
      controls: [{
        id: 1,
        iconPath: '../../images/sousou.png',
        position: {
          left: 0,
          top: 300 - 50,
          width: 50,
          height: 50
        },
        clickable: true
      }],
      jllist:[],
      searchId:'',
      type:0,
      detail:{},
      article:"",
      imgmode:{
        mode:"widthFix",
        domain:conf.IP
      }
    }
  },
  created () {
    //
    this.getCenterAndStationList();
  },
  mounted(){
    this.getLocation();
  },
  methods:{
    getLocation(){
      var that=this;
      wx.getLocation({
        type: 'wgs84',
        success (res) {//获取当前位置
          // console.log(JSON.stringify(res))
          that.longitude=res.longitude;
          that.latitude=res.latitude;
          wx.getStorage({
            key: 'token',
            success(res2) {
              let Location={
                token:res2.data,
                lon:res.longitude,//经度
                lat:res.latitude//维度
              }
              wx.setStorage({
                key: 'Location',
                data: Location
              })
            }
          })
        }
      })
    },
    bindmarkertap(e){
      this.setfirstflag(true);
      this.settwoflag(false);
      this.setthreeflag(true);
      //console.log(e.mp.markerId)//获取markerId
      this.goSelect(e.mp.markerId);
    },
    closeBox(){
      this.setboxflag(true);
    },
    goSelect(id){
      console.log(id)
      var that=this;
      var url="";
      var data={};
      this.settwoflag(false);
      this.setthreeflag(true);
      //console.log(this.type)
      switch (this.type){
        case 1:
        url=`/stddj-gzgj/servlet/map.action?method=getCenterDetail`;
        data={
          lon:that.longitude,
          lat:that.latitude,
          centerId:id
        }
        that.ajaxdetail(url,data);
          break;
        case 2:
          url=`/stddj-gzgj/servlet/map.action?method=getStationDetail`;
          data={
            lon:that.longitude,
            lat:that.latitude,
            stationId:id
          }
          that.ajaxdetail(url,data);
          break;
        case 3:
          url=`/stddj-gzgj/servlet/unit.action?method=getUnitDetail`;
          data={
            lon:that.longitude,
            lat:that.latitude,
            unitId:id
          }
          wx.request({
            url:`${conf.HOST}/stddj-gzgj/servlet/unit.action?method=getUnitDetail`,
            data:data,
            success(res){
              //console.log(JSON.stringify(res.data));
              that.detail={
                "ORG_ID": res.data[0].UNIT_ID,
                "ORG_NAME": res.data[0].UNIT_NAME,
                "ADDR": res.data[0].UNIT_ADDR,
                "ORG_TEL": res.data[0].UNIT_TEL,
                "IMG": res.data[0].UNIT_THUMB_IMG,
                "LAT": res.data[0].LAT,
                "LON": res.data[0].LON,
                "CENTER_ORG_ID": res.data[0].UNIT_ORG_ID,
                "CONTENT": res.data[0].UNIT_CONTENT,
                "DISTANCE": res.data[0].DISTANCE,
              }
              //console.log(JSON.stringify(that.detail))
              var html0 =res.data[0].UNIT_CONTENT;
              var html1 = html0.replace(/\s+style="[^"]*"/g,'')
              var newHtml = html1.replace(/<img/g, '<img style="max-width:100%;"')
              that.article=`<div style="font-size: 30rpx !important; ">${newHtml}</div>`;
            }
          })
          break;
        default:
          url=`/stddj-gzgj/servlet/map.action?method=getOrgDetail`;
          data={
            lon:that.longitude,
            lat:that.latitude,
            orgId:id
          }
          that.ajaxdetail(url,data);
          break;
      }
    },
    ajaxdetail(url,data){
      //console.log(data)
      var that=this;
      wx.request({
        url:`${conf.HOST}${url}`,
        data:data,
        success(res){
         //console.log(JSON.stringify(res.data));
          that.detail=res.data;
          if(res.data.CONTENT){
            var html0 =res.data.CONTENT;
            var html1 = html0.replace(/\s+style="[^"]*"/g,'');
            var newHtml = html1.replace(/<img/g, '<img style="max-width:100%;"');
            that.article=`<div style="font-size:30rpx !important;">${newHtml}</div>`;
            //console.log(that.article);
          }else{
            that.article=""
          }

        }
      })

    },
    Call(number){
      wx.makePhoneCall({
        phoneNumber:number
      });
    },
    goMapSearch(){
      wx.removeStorage({
        key: 'searchId',
        success(res) {
          //console.log(res.data)
        }
      }),
        this.settwoflag(false);
        this.setthreeflag(false);
      wx.navigateTo({
        url:`/pages/mapsearch/main`
      });
    },
    goResult(index){
      //console.log(index);
      this.type=index;
      var that=this;
      var url="";
      switch(index){
        case 1:
          //获取中心列表
          url="/stddj-gzgj/servlet/map.action?method=getCenterList";
          that.ajax(url);
          break;
        case 2:
          //获取服务站列表
          url="/stddj-gzgj/servlet/map.action?method=getStationList";
          that.ajax(url);
          break;
        case 3:
          //获取重点单位列表
          url="/stddj-gzgj/servlet/map.action?method=getUnitList";
          that.ajax(url);
          break;
        case 4:
          //获取党支部列表
          url="/stddj-gzgj/servlet/map.action?method=getZBList";
          that.ajax(url);
          break;
        case 5:
          //获取党总支列表
          url="/stddj-gzgj/servlet/map.action?method=getDZZList";
          that.ajax(url);
          break;
        case 6:
        //获取党工委列表
          url="/stddj-gzgj/servlet/map.action?method=getDWList";
          that.ajax(url);
          break;
      }
      this.setfirstflag(true);
      this.settwoflag(true);
    },
    ajax(url,data){
      var that=this;
      wx.request({
        url:`${conf.HOST}${url}`,
        data:{
          lon:that.longitude,
          lat:that.latitude
        },
        success(res){
         //console.log(JSON.stringify(res));
          that.jllist=res.data;
          that.initList(res.data)
        }
      })
    },
    goMore(id){
      //console.log(this.type);
      switch (this.type){
        case 1:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=0&UNIT_ID=${id}`
          });
          break;
        case 2:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=1&UNIT_ID=${id}`
          });
          break;
        case 3:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=2&UNIT_ID=${id}`
          });
          break;
        case 4:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=4&UNIT_ID=${id}`
          });
          break;
        case 5:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=4&UNIT_ID=${id}`
          });
          break;
        case 6:
          wx.navigateTo({
            url:`/pages/serverDetail/main?type=4&UNIT_ID=${id}`
          });
          break;
      }

    },
    toBeforeone(){
      this.setfirstflag(false);
      this.settwoflag(false);
      this.setthreeflag(false);
    },
    toBeforetwo(){
      this.settwoflag(true);
      this.setthreeflag(false);
    },
    getCenterAndStationList(){
      var that=this;
      //获取街道中心和党群服务站列表
      wx.request({
        url:`${conf.HOST}/stddj-gzgj/servlet/map.action?method=getCenterAndStationList`,
        data:{
          lon:that.longitude,
          lat:that.latitude
        },
        success(res){
          //console.log(JSON.stringify(res.data))
          var list=that.initList(res.data);
        }
      })
    },
    initList(list){
      var that=this;
      var map=[];
      //console.log(JSON.stringify(list))
      for(var i=0;i<list.length;i++){
        map.push({
          iconPath: "/images/marker.png",
          id: list[i].ORG_ID,
          longitude: list[i].LON,
          latitude: list[i].LAT,
          width: 30,
          height: 38,
          callout:{
            content:list[i].ORG_NAME,
            bgColor:'#ffffff',
            padding:6,
            borderColor:"#ffffff",
            borderRadius:5
          }
        })
      }
      that.markers=map;//初始化地图标志
      return map;
    },
    ...mapMutations({
      setboxflag:'SET_BOXFLAG',
      setfirstflag: 'SET_FIRSTFLAG',
      settwoflag: 'SET_TWOFLAG',
      setthreeflag: 'SET_THREEFLAG'
    })
  },
  computed:{
    boxflaghide(){
      return this.boxflag?'boxhide':' '
    },
    firsthide(){
      return this.firstflag?'first':' '
    },
    twohide(){
      return !this.twoflag?'two':' '
    },
    threehide(){
      return !this.threeflag?'three':' '
    },
    ...mapGetters({
      boxflag:"boxflag",
      firstflag:"firstflag",
      twoflag:"twoflag",
      threeflag:"threeflag"
    })

  },
  onShow(){
    let pages = getCurrentPages();//获取所有页面
    let prevPage = pages[ pages.length - 1 ];//获取当前页面的data里的数据
    // console.log(JSON.stringify(prevPage.data.searchId));//获取searchID
    // this.$nextTick(function(){
    //   this.searchId=prevPage.data.searchId;
    // });
    // console.log(this.searchId)
    var that=this;
    wx.getStorage({
      key: 'type',
      success(res) {
        //console.log(res.data);
        that.goResult(res.data);
      },
      fail(){
        wx.getStorage({
          key:'mapSearch',
          success(res){
            //console.log(JSON.stringify(res.data))
            that.jllist=res.data;
            that.initList(res.data)
          }
        })
      }
    })
  },
  onHide(){
    wx.removeStorage({
      key: 'type',
      success(res) {
        //console.log(res.data)
        wx.removeStorage({
          key: 'type',
          success(ret) {
            //console.log(res.data)
          }
        })
      }
    })
  },
  onUnload(){
    this.setboxflag(false);
    this.setfirstflag(false);
    this.settwoflag(false);
    this.setthreeflag(false);
  },
  destroyed (){

  },
  components: {
    wxParse
  }
}
</script>

<style scoped lang="less">
  @import "../../common/css/font/iconfont.css";
  @import "../../common/css/less/base";
  .djmap{
    width: 100%;
    height: 100vh;
    .scroll{
      width: 100%;
      max-height: 500rpx;
      overflow: scroll;
    }
    .sbzj{
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    }
    .search{
      width: 100%;
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
        .text{
          width: 100%;
          font:28rpx "黑体";
          line-height:60rpx;
          color:#bfbfbf;
        }
        input::placeholder{
          color:#bfbfbf;
        }
        .iconfont{
          position:absolute;
          width:52rpx;
          height:32rpx;
          left:14rpx;
          color:#bfbfbf;
          top:14rpx;
        }
      }
      .cancel{
        font:28rpx "黑体";
        color:#bfbfbf;
        padding-right:14rpx;
        line-height:60rpx;
      }
    }
    .search_box{
      position: fixed;
      left: 0;
      bottom: 0;
      background: #fff;
      width: 100%;
      border-radius: 10rpx 10rpx 0 0;
      padding-top:14rpx;
      .content{
        width: 680rpx;
        margin: 0 auto;
        .title{
          width: 100%;
          height: 68rpx;
          line-height: 68rpx;
          font:30rpx "黑体";
          display: flex;
          align-items: center;
          justify-content: space-between;
          font-weight: bold;
          margin-bottom: 40rpx;
          position: relative;
          .iconfont{
            width: 34rpx;
            height: 34rpx;
            margin-right: 10rpx;
            color:#999999;
          }
          .borderB{
            position: absolute;
            bottom: 0;
            left:0;
            width: 100%;
            height: 1rpx;
            background: #f2f2f2;
          }
          .back{
            display: flex;
            align-items: center;
            font:22rpx "黑体";
            color:#bfbfbf;
            .iconfont{
              width: 19rpx;
              height: 18rpx;
              margin-left: 10rpx;
            }
          }
        }
          .resultlist{
            display: inline-block;
            width: 210rpx;
            border:1rpx solid #bfbfbf;
            font:28rpx "黑体";
            color:#666666;
            float: left;
            border-radius:8rpx;
            text-align: center;
            margin-bottom: 30rpx;
            padding:16rpx 0;
          }
          .resultlist:last-child{
            margin-right: 0;
          }
        .borderB{
          position: absolute;
          bottom: 0;
          left:0;
          width: 100%;
          height: 1rpx;
          background: #f2f2f2;
        }
          .jllist{
            width: 100%;
            height: 174rpx;
            overflow: hidden;
            display: flex;
            align-items: center;
            position: relative;
            .disimg{
              width: 160rpx;
              height: 130rpx;
              border-radius:10rpx;
              margin-right: 30rpx;
              overflow: hidden;
            }
            .center{
              width: 390rpx;
              height: 130rpx;
              display: flex;
              flex-direction: column;
              justify-content: space-between;
              .name{
                font:30rpx "黑体";
              }
              .addr,.tel{
                font:22rpx "黑体";
                color:#7b8086;
              }
              .addr{
                margin-bottom: 5rpx;
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
              }
            }
            .phone{
              flex:1;
              width: 100%;
              height:130rpx;
              position: relative;
              .icon{
                width: 80rpx;
                height: 48rpx;
                position: absolute;
                bottom: 6rpx;
                right: 10rpx;
              }
            }
          }
        .pingjia{
          width: 100%;
          .jianjie{
            width: 100%;
            height: 110rpx;
            font:30rpx "黑体";
            line-height:110rpx;
            font-weight: bold;
          }
          .textBox{
            width: 680rpx;
            .text{
              display: block;
              width: 680rpx;
              height: 280rpx;
              word-wrap:break-word;
              word-break:break-all;
              text-align: justify;
              font:30rpx "黑体";
              line-height: 50rpx;
              white-space: pre-wrap;
              overflow: hidden;
            }
            .guodu{
              width: 100%;
              height: 230rpx;
              position: absolute;
              bottom: 0;
              left: 0;
              text-align: center;
              color:#7b8086;
            }
          }
        }
      }

      .first{
        display: none;
      }
      .two{
        display: none;
      }
      .three{
        display: none;
      }
    }
    .boxhide{
      display:none;
    }
  }
</style>
