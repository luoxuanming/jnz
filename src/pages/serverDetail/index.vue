<template>
  <div class="serverDetail">
    <scroll-view :scroll-y="true" class="scroll">
      <div class="head">
        <div class="content">
          <!--<img v-if="infos.UNIT_THUMB_IMG" :src="infos.UNIT_THUMB_IMG" alt="" class="serverbg">-->
          <!--<img v-else src="../../images/serverDetail.png" alt="" class="serverbg">-->
          <div class="top_img">
            <img src="../../images/serverDetail.png" alt="" class="serverbg">
            <div class="layer">
              <p class="org_name" v-if="infos.UNIT_NAME!=null">
                {{infos.UNIT_NAME}}
              </p>
              <p class="org_name" v-if="infos.UNIT_NAME==null">
                江南中街道党群服务中心
              </p>
            </div>
          </div>
          <div class="addr">
            <dl>
              <dt>{{infos.DISTANCE}}km <span v-if="infos.UNIT_ADDR">| {{infos.UNIT_ADDR}}</span></dt>
              <dd>联系电话：{{infos.UNIT_TEL}}</dd>
            </dl>
            <i class="iconfont icon-dianhua" @click="Call(infos.UNIT_TEL)"></i>
          </div>
        </div>
      </div><!--头部END-->
      <div class="hr" v-if="infos.UNIT_CONTENT"></div>
      <div class="brief" v-if="infos.UNIT_CONTENT" :class="flag||type==1?'brief_more':' '">
        <div class="content">
          <h3>简介</h3>
          <!--<rich-text :nodes="infos.UNIT_CONTENT"></rich-text>-->
          <wxParse :content="infos.UNIT_CONTENT" :imageProp="imgmode" />
          <div class="guodu" @click="toMore" :class="flag || type==1 ?'gd_none':' '">
            <span>查看更多 </span><i class="iconfont icon-jiantou-copy"></i>
          </div>
        </div>
      </div><!--简介END-->
      <div v-if="type!=2">
        <div class="hr"></div>
        <div class="gonggao">
          <div class="content">
            <h3>服务公告</h3>
            <infolist :list="fwlist"></infolist>
          </div>
        </div><!--服务公告END-->
        <div class="hr" v-if="members.length"></div>
        <div class="members" v-if="members.length">
          <div class="content">
            <h3>委员会成员</h3>
            <div class="member_box">
              <scroll-view :scroll-x="true" class="scroll_member">
                <div class="card" v-for="(item,index) in members" :key="index">
                  <dl>
                    <dt>{{item.USER_NAME}}</dt>
                    <dd>{{item.POST_NAME}}</dd>
                  </dl>
                  <span class="biaozhi"></span>
                </div>
              </scroll-view>
            </div>
          </div>
        </div><!--委员会成员END-->
        <div class="hr"></div>
        <div class="fuwuzhan">
          <div class="content">
            <h3>社区党群服务站</h3>
            <scroll-view :scroll-x="true" class="scroll-fwz">
              <div class="show" v-for="(item,index) in shows" :key="index">
                <img :src="item.IMG" alt="" class="fwz_pic">
                <p>{{item.ORG_NAME}}</p>
              </div>
            </scroll-view>
          </div>
        </div><!--社区党群服务站END-->
        <div class="hr"></div>
        <div class="zddw">
          <div class="content">
            <h3 class="zddwh3">辖区重点单位<div class="more" @click="moreZddw" v-if="zdlist.length>3">更多<i class="iconfont icon-jiantou"></i></div></h3>
            <div class="zdlist" v-for="(item,index) in zdlist" :key="index" v-if="index<3">
              <dl>
                <!--<dt>行政单位</dt>-->
                <dd>{{item.ORG_NAME}}</dd>
              </dl>
            </div>
            <!--<div class="zdlist">-->
              <!--<dl>-->
                <!--<dt>机关单位</dt>-->
                <!--<dd>单位名称占位单位名称占位单位名称占位</dd>-->
              <!--</dl>-->
            <!--</div>-->
            <!--<div class="zdlist">-->
              <!--<dl>-->
                <!--<dt>私企单位</dt>-->
                <!--<dd>单位名称占位单位名称占位单位名称占位</dd>-->
              <!--</dl>-->
            <!--</div>-->
          </div>
        </div><!--辖区重点单位END-->
      </div>
    </scroll-view>
  </div>
</template>

<script>
import infolist from '../../base/infoList/infoList'
import wxParse from 'mpvue-wxparse'
import * as conf from '../../utils/config'
  export default {

    data () {
      return {
        infos:"",
        type:"",
        flag:false,
        article:"",
        imgmode:{
          mode:"widthFix",
          domain:conf.IP
        },
        cardlist:[1,2],
        pastlist:[1,2],
        members:[],
        shows:[],
        zdlist:[],
        fwlist:[
          {
            ALIAS_TITLE:"深圳开发开发40年：“烂泥镀”摇变“最摩登”（专题文章标题）",
            MODIFY_TIME:"2018-09-15 17:00",
            READ_COUNT:2323,
            NEWS_THUMB_IMG:"../../images/default_img.jpg"
          },
          {
            ALIAS_TITLE:"深圳开发开发40年：“烂泥镀”摇变“最摩登”（专题文章标题）",
            MODIFY_TIME:"2018-09-15 17:00",
            READ_COUNT:2323,
            NEWS_THUMB_IMG:"../../images/default_img.jpg"
          }
        ]
      }
    },

    created () {

    },
    methods:{
      toMore(){
        this.flag=true;
      },
      Call(number){
        wx.makePhoneCall({
          phoneNumber:number
        });
      },
      ajax(index,id){
        //console.log(index+"*"+id)
        var that=this;
        var data;
        var url="";
        wx.getStorage({
          key: 'Location',
          success(ret) {
            switch (index){
              case "0":
                //获取党群中心详情
                data= {
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                  centerId:id
                }
                url="/stddj-gzgj/servlet/map.action?method=getCenterDetail";
                that.ajaxReq(url,data);
                break;
              case "1":
                //获取党群服务站详情
                data= {
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                  stationId:id
                }
                url="/stddj-gzgj/servlet/map.action?method=getStationDetail";
                that.ajaxReq(url,data);
                break;
              case "2":
                //获取重点单位详情
                data= {
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                  unitId:id
                }
                url="/stddj-gzgj/servlet/unit.action?method=getUnitDetail";
                wx.request({
                  url: `${conf.HOST}${url}`,
                  data: data,
                  header: {
                    'content-type': 'application/json' // 默认值
                  },
                  success (res) {
                    //console.log(JSON.stringify(res.data[0]))
                    that.infos=res.data[0];
                    var html0 =res.data[0].UNIT_CONTENT;
                    var html1 = html0.replace(/\s+style="[^"]*"/g,'');
                    var newHtml = html1.replace(/<img/g, '<img style="max-width:100%;"')
                    that.article=`<div style="font-size:30rpx !important;">${newHtml}</div>`;
                  }
                });
                break;
              default:
                //党总支详情
                data= {
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                  orgId:id
                }
                url="/stddj-gzgj/servlet/map.action?method=getOrgDetail";
                that.ajaxReq(url,data);
                break;

            }

          }
        })
      },
      ajaxReq(url,data){
        var that=this;
        wx.request({
          url: `${conf.HOST}${url}`,
          data: data,
          header: {
            'content-type': 'application/json' // 默认值
          },
          success (res) {
            //that.infos=res.data[0];
            console.log(JSON.stringify(res.data.ORG_TEL))
            that.infos={
              "UNIT_ID":res.data.ORG_ID,
              "UNIT_NAME":res.data.ORG_NAME ,
              "UNIT_ADDR":res.data.ADDR,
              "UNIT_CONTENT":res.data.CONTENT,
              "UNIT_THUMB_IMG":res.data.IMG,
              "UNIT_TEL":res.data.ORG_TEL,
              "LAT":res.data.LAT,
              "LON": res.data.LON,
              "POSTLIST": res.data.postList,
              "DISTANCE":res.data.DISTANCE
            };
            that.members=res.data.postList;
            if(res.data.CONTENT){
              var html0 =res.data.CONTENT;
              var html1 = html0.replace(/\s+style="[^"]*"/g,'')
              var newHtml = html1.replace(/<img/g, '<img style="max-width:100%;"')
              that.article=`<div style="font-size:30rpx !important;">${newHtml}</div>`;
            }else{
              that.article=""
            }

          }
        });
      },
      getStationDetail(){
        //获取服务站列表
        var that=this;
        wx.getStorage({
            key: 'Location',
            success(ret) {
              wx.request({
                url:`${conf.HOST}/stddj-gzgj/servlet/map.action?method=getStationList`,
                data:{
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                },
                success(res){
                  //console.log(JSON.stringify(res.data))
                  that.shows=res.data;
                }
              })
            }
        })
      },
      getUnitList(){
        //获取重点单位列表
        var that=this;
        wx.getStorage({
            key: 'Location',
            success(ret) {
              wx.request({
                url:`${conf.HOST}/stddj-gzgj/servlet/map.action?method=getUnitList`,
                data:{
                  lon:ret.data.lon,
                  lat:ret.data.lat,
                },
                success(res){
                  //console.log(JSON.stringify(res.data))
                  that.zdlist=res.data;
                }
              })
            }
        })
      },
      moreZddw(){
        //查看更多重点单位
        wx.navigateTo({
          url:`/pages/zddw/main`
        })
      },
      getFwList(){
        var that=this;
        wx.request({
          url:`${conf.HOST}/cloud-app/servlet/dynamic.action?method=getDynamicByChannel`,
          data:{
            pageIndex:1,
            pageSize:10,
            CHANNEL_ID:110037
          },
          success(res){

            that.fwlist=res.data;
          }
        })
      }
    },
    onLoad(id){
      this.type=id.type;
      //console.log(id.type+":"+id.UNIT_ID)
      this.ajax(id.type,id.UNIT_ID);
      this.getStationDetail();
      this.getUnitList();
      this.getFwList();
    },
    components: {
      infolist,
      wxParse
    },
    onUnload(){
      this.flag=false;
    }
  }
</script>

<style scoped lang="less">
  @import url("~mpvue-wxparse/src/wxParse.css");
  @import "../../common/css/font/iconfont.css";
  .serverDetail{
    width: 100%;
    height: 100vh;
    .scroll{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
      .content{
        width: 668rpx;
        height: auto;
        margin:0 auto;
        h3{
          width: 100%;
          height: 92rpx;
          font:32rpx "黑体";
          line-height: 92rpx;
          font-weight: bold;
          display: flex;
          justify-content: space-between;
          align-items: center;
          .more{
            font:22rpx "黑体";
            color:#7f8699;
            display: flex;
            align-items: center;
            i{
              margin-left: -4rpx;
            }
          }
        }
      }
      .hiddenBox{
        display: none;
      }
      .hr{
        width: 100%;
        height:14rpx;
        background:#f6f8fd;
      }
      .head{
        width: 100%;
        height: 318rpx;
        background: #fff;
        padding-top:8rpx;
        padding-bottom:24rpx;
        box-sizing: border-box;
        .top_img{
          width: 100%;
          height: 200rpx;
          margin-bottom: 20rpx;
          overflow: hidden;
          position: relative;
          .serverbg{
            width: 100%;
            height: 200rpx;
            border-radius:10rpx;
          }
          .layer{
            width: 100%;
            height: 100%;
            position: absolute;
            left: 0;
            top:48rpx;
            p{
              font:36rpx "微软雅黑";
              font-weight: bold;
              color:#fff;
              text-align: center;
            }
          }
        }
        .addr{
          display: flex;
          justify-content: space-between;
          dl{
            font:22rpx "黑体";
            color:#7f8699;
            dt{
              margin-bottom: 8rpx;
            }
            dd{}
          }
          i{
            font-size: 50rpx;
            color:#7f8699;
          }
        }
      }
      .brief{
        width: 100%;
        height: 258rpx;
        overflow: hidden;
        background: #fff;
        padding:22rpx 0;
        box-sizing: border-box;
        position: relative;
        p{
          font:32rpx "黑体";
          text-align: justify;
          line-height: 50rpx;
        }
        .guodu{
          width: 100%;
          height: 118rpx;
          background:
            linear-gradient(to bottom,
            rgba(255,255,255,0),
            rgba(255,255,255,0.8),
            rgba(255,255,255,1),
            rgba(255,255,255,1),
            rgba(255,255,255,1));
          position: absolute;
          bottom: 0;
          left: 0;
          font:24rpx "黑体";
          line-height:164rpx;
          text-align: center;
          color:#7f8699;
          display: flex;
          justify-content: center;
        }
        .gd_none{
          display: none;
        }
      }
      .brief_more{
        height:auto;
      }
      .gonggao{
        width: 100%;
        background: #fff;
        padding:22rpx 0;
        padding-bottom: 22rpx;
      }
      .members{
        width: 100%;
        background: #fff;
        padding-top:22rpx;
        box-sizing: border-box;
          .member_box{
            width: 100%;
            height:160rpx;
            margin-top:10rpx;
            white-space: nowrap;
            .scroll_member{
              width: 100%;
              height:160rpx;
              white-space: nowrap;
              overflow: hidden;
            .card{
              width: 182rpx;
              height: 110rpx;
              border:1rpx solid #f9c8c8;
              box-shadow: 0 0 3rpx #f9c8c8;
              border-radius: 10rpx;
              padding-top:12rpx;
              box-sizing: border-box;
              display: inline-block;
              text-align: center;
              position: relative;
              margin-right: 24rpx;
              dl{
                dt{
                  font:32rpx "微软雅黑";
                  color:#3f3f3f;
                  margin-bottom: 10rpx;
                }
                dd{
                  font:20rpx "黑体";
                }
              }
              .biaozhi{
                width: 38rpx;
                height: 10rpx;
                background: #d40303;
                position: absolute;
                top:20rpx;
                left: -1rpx;
              }
            }

          }

        }
      }
      .fuwuzhan{
        width: 100%;
        height: 368rpx;
        background: #fff;
        box-sizing: border-box;
        padding-top:22rpx;
        padding-bottom: 40rpx;
        white-space: nowrap;
        .show{
          width: 254rpx;
          height: 210rpx;
          margin-top:10rpx;
          display: inline-block;
          margin-right:36rpx;
          .fwz_pic{
            width: 254rpx;
            height: 150rpx;
            margin-bottom:10rpx;
            border-radius: 5rpx;
          }
          p{
            font:28rpx "微团雅黑";
            color:#333333;
          }
        }
      }
      .zddw{
        width: 100%;
        background: #fff;
        padding:22rpx 0;
        .zddwh3{
          margin-bottom: 10rpx;
        }
        .zdlist{
          width: 100%;
          height: 160rpx;
          box-sizing: border-box;
          border:1rpx solid #d7dce9;
          border-radius:10rpx;
          background: url("../../images/zddw.png") no-repeat;
          background-size:183rpx 129rpx;
          background-position: bottom right 40rpx;
          padding-left:46rpx;
          box-sizing: border-box;
          display: flex;
          align-items: center;
          margin-bottom: 30rpx;
          dl{
            width: 400rpx;
            dt{
              font:22rpx "黑体";
              color:#7f8699;
              margin-bottom: 10rpx;
            }
            dd{
              font:30rpx "微软雅黑";
              color:#333333;
              height: 80rpx;
              overflow: hidden;
            }
          }
        }
      }
    }
  }
</style>
