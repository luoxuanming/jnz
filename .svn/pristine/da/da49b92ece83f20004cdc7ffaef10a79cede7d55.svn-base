import * as conf from './config'

// export default function ajax(options){
//   var that=this;
//   wx.request({
//     //登录来获取token值
//     url: conf.HOST+"/cloud-app/servlet/login.action?method=login",
//     data: {
//       userAccount:that.userAccount,
//       userPwd:that.userPwd
//     },
//     header: {
//       'content-type': 'application/json' // 默认值
//     },
//     success (ret) {
//       that.setToken(ret.data.userInfo.token);
//       let token=ret.data.userInfo.token;
//       wx.request({
//         url: conf.HOST+options.url,
//         data:options.data,
//         header: {
//           'content-type': 'application/json',// 默认值
//           'Authorization': token
//         },
//         success (res) {
//             options.success=JSON.parse(res);
//         }
//       });
//     }
//   });
// }

function withData(param){
  return param < 10 ? '0' + param : '' + param;
}
function getLoopArray(start,end){
  var start = start || 0;
  var end = end || 1;
  var array = [];
  for (var i = start; i <= end; i++) {
    array.push(withData(i));
  }
  return array;
}
function getMonthDay(year,month){
  var flag = year % 400 == 0 || (year % 4 == 0 && year % 100 != 0), array = null;

  switch (month) {
    case '01':
    case '03':
    case '05':
    case '07':
    case '08':
    case '10':
    case '12':
      array = getLoopArray(1, 31)
      break;
    case '04':
    case '06':
    case '09':
    case '11':
      array = getLoopArray(1, 30)
      break;
    case '02':
      array = flag ? getLoopArray(1, 29) : getLoopArray(1, 28)
      break;
    default:
      array = '月份格式不正确，请重新输入！'
  }
  return array;
}
function getNewDateArry(){
  // 当前时间的处理
  var newDate = new Date();
  var year = withData(newDate.getFullYear()),
    mont = withData(newDate.getMonth() + 1),
    date = withData(newDate.getDate()),
    hour = withData(newDate.getHours()),
    minu = withData(newDate.getMinutes()),
    seco = withData(newDate.getSeconds());

  return [year, mont, date, hour, minu, seco];
}
export default function dateTimePicker(startYear,endYear,date) {
  // 返回默认显示的数组和联动数组的声明
  var dateTime = [], dateTimeArray = [[],[],[],[],[],[]];
  var start = startYear || 1978;
  var end = endYear || 2100;
  // 默认开始显示数据
  var defaultDate = date ? [...date.split(' ')[0].split('-'), ...date.split(' ')[1].split(':')] : getNewDateArry();
  // 处理联动列表数据
  /*年月日 时分秒*/
  dateTimeArray[0] = getLoopArray(start,end);
  dateTimeArray[1] = getLoopArray(1, 12);
  dateTimeArray[2] = getMonthDay(defaultDate[0], defaultDate[1]);
  dateTimeArray[3] = getLoopArray(0, 23);
  dateTimeArray[4] = getLoopArray(0, 59);
  dateTimeArray[5] = getLoopArray(0, 59);

  dateTimeArray.forEach((current,index) => {
    dateTime.push(current.indexOf(defaultDate[index]));
  });

  return {
    dateTimeArray: dateTimeArray,
    dateTime: dateTime
  }
}
// module.exports = {
//   dateTimePicker: dateTimePicker,
//   getMonthDay: getMonthDay
// }
