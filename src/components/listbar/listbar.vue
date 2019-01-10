<template>
  <div class="listbar">
    <ul>
      <li @click="goDjMap">
        <img src="../../images/listbar03.png" class="list_icon" alt="">
        <p>党建地图</p>
        <span>找到身边的党组织</span>
      </li>
      <li @click="goVolunteer">
        <img src="../../images/listbar01.png" class="list_icon" alt="">
        <p>志愿活动</p>
        <span>我志愿,我快乐</span>
      </li>
      <li @click="goPower(7)">
        <img src="../../images/listbar02.png" class="list_icon" alt="">
        <p>榜样的力量</p>
        <span>学榜样，做榜样</span>
      </li>
      <li @click="goZjdx">
        <img src="../../images/listbar04.png" class="list_icon" alt="">
        <p>指尖党校</p>
        <span>学习也能赚积分</span>
      </li>
      <li @click="goGzGj">
        <img src="../../images/listbar06.png" class="list_icon" alt="">
        <p>共建共治</p>
        <span>示范引领民意通达</span>
      </li>
      <li @click="goWyBs">
        <img src="../../images/listbar05.png" class="list_icon" alt="">
        <p>我要办事</p>
        <span>党务政务一“点”不远</span>
      </li>
    </ul>
   </div>
</template>

<script>
    export default {
        data(){
          return{

          }
        },
        methods:{
          goDjMap(){
            wx.navigateTo({
              url:`/pages/djmap/main`
            })
          },
          goPower(id){
            wx.navigateTo({
              url:`/pages/examPower/main?CHANNEL_ID=`+id
            })
          },
          goVolunteer(){
            wx.navigateTo({
              url:`/pages/volunteerActivty/main`
            })
          },
          goGzGj(){
            wx.navigateTo({
              url:`/pages/gzgz/main`
            })
          },
          goWyBs(){
            wx.navigateTo({
              url:`/pages/wybs/main`
            })
          },
          goZjdx(){
            wx.navigateTo({
              url:`/pages/zjdx/main`
            })
          }
        }
    }
</script>

<style scoped lang="less">
  .listbar{
    width:692rpx;
    background: #fff;
    margin:0 auto;
    ul{
      overflow: hidden;
      li{
        width:230rpx;
        text-align:center;
        margin-bottom:40rpx;
        float: left;
        display: flex;
        flex-direction: column;
        justify-content: center;
        height:150rpx;

        .list_icon{
          width:58rpx;
          height:54rpx;
          margin:0 auto;
          margin-bottom:8rpx;
        }
        p{
          font:30rpx "微软雅黑";
          letter-spacing: -2rpx;
        }
        span{
          font:20rpx "黑体";
          color:#7f8699;
          /*margin-top:5rpx;*/
        }
      }
    }
  }
</style>
