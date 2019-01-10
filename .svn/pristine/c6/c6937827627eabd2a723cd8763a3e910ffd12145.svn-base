<template>
  <div class="outlink">
    <scroll-view :scroll-y="true" class="scroll">
        <web-view :src="url"></web-view>
    </scroll-view>
  </div>
</template>

<script>
  import * as conf from '../../utils/config'

  export default {
    data () {
      return {
         url:`${conf.HOST}/cloud-app/app/html/volunteer/activityDetail.html`
      }
    },

    created () {

    },
    onLoad(params){
      console.log(params.USER_CODE+":"+params.USER_ID+":"+params.m_USER_ID+":"+params.m_ORG_NAME);
      let {type}=params;
      const USER_CODE=conf.userAccount;
      const HOST=conf.HOST;
      switch (type){
        case '0':
          //志愿详情
          this.url=`${HOST}/cloud-app/app/html/volunteer/activityDetail.html?USER_CODE=${USER_CODE}&activityId=${params.ACTIVITY_ID}`
          break;
        case '1':
          //课程列表
          this.url=`${HOST}/cloud-app/app/html/study1/course-recommen.html?CAT_ID=${params.CAT_ID}`
          break;
        case '2':
          //课程详情
          this.url=`${HOST}/cloud-app/app/html/study1/study-videoDetail.html?DOC_ID=${params.DOC_ID}&RES_ID=${params.RES_ID}&CAT_ID=${params.CAT_ID}&m_ORG_ID=${params.m_ORG_ID}&m_USER_NAME=${params.m_USER_NAME}&m_USER_ID=${params.m_USER_ID}&m_ORG_NAME=${params.m_ORG_NAME}`
          break;
        case '3':
          //政务
          this.url=`http://wx.haizhu.gov.cn/jms-web/depends/hzwx/index/freeIndex.jsp`
          break;
        case '4':
          //答题闯关
          this.url=`${HOST}/cloud-app/pages/html/game/practice2.html?userCode=${params.USER_CODE}&orgId=${params.ORG_ID}`
          break;
        case '5':
          //积分
          this.url=`${HOST}/cloud-app/app/html/jf/Jfindex.html`
          break;
      }
    },
    components: {

    },
  }
</script>

<style scoped lang="less">
  .outlink{
    width: 100%;
    height: 100vh;
    .scroll{
      width: 100%;
      height: 100vh;
      overflow: hidden;
      background: url("../../images/logo.png") no-repeat;
      background-size: 363rpx 70rpx;
      background-position: center bottom 30rpx;
    }
  }
</style>
