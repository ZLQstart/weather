
<template>
  <div id="index">
    <div class="content">
      <div class="city">{{weatherList.city}}&nbsp&nbsp&nbsp{{weatherList.update_time}}</div>

      <div class="center">
        <div class="tem">{{weatherList.data[0].tem}}</div>
        <div class="tip">{{weatherList.data[0].air_tips}}</div>
        <div class="lastTem">{{weatherList.data[0].wea}}</div>

        <div class="future">
          <div class="box" v-for="(item,index) in futureList" :key="index">
            <div>{{item.day}}</div>
            <div>{{item.week}}</div>
            <div class="zt">{{item.zt}}</div>
            <div>高温{{item.tem1}}</div>
            <div>低温{{item.tem2}}</div>
            <div class="zt">{{item.win[0]}}</div>
            <div class="zt">{{item.win_speed}}</div>
          </div>
        </div>
      </div>

      <div class="choose">
        <input placeholder="请输入城市名称" v-model="city">
        <mt-button type="primary">查询</mt-button>
      </div>
    </div>
  </div>
</template>

<script>
import { Button } from 'mint-ui';

import api from './../axios/api.js'

export default {
  data () {
    return {
      city:'',
      weatherList:[],
      // futureList:[{
      //   data:"6",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },{
      //   data:"6日",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },{
      //   data:"6日",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },{
      //   data:"6日",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },{
      //   data:"6日",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },{
      //   data:"6日",
      //   week:"周一",
      //   zt:"晴",
      //   high:"19",
      //   bottom:"12",
      //   f:"南风",
      //   fl:"微风级"
      // },]
    }
  },
  created () {
    this.getDatas()
  },
  methods: {
    getDatas: function() {

      api.getData('https://www.tianqiapi.com/api/', 'version=v1')
        .then(res => {
          console.log(res)
          this.weatherList = res
          this.futureList=res.data
        }).catch(err => {
          console.log(err)
        })
    }
    
  }
  
}
</script>

<style lang="less">
// @color-primary: #79c3f2;
// .mint-button--primary {
//     background-color: @color-primary;
// }
body{
  background-color: #79c3f2;
  box-sizing: border-box;
  width: 100%;
  height: auto;
  min-height: 100%;
  display: flex;
  flex-direction: column;
}
#index{
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: column;

  .content {
    margin: 10px auto;
    padding: 20px;
    width: 800px;
    height: auto;
    background-color: #fff;

    .city {
      width: 100%;
      height: auto;
      text-align: left;
      padding-bottom: 20px;
    }
    .center {
      width: 100%;
      height: auto;
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;

      .tem {
        font-size: 40px;
        padding-bottom: 10px;
      }

      .lastTem {
        border: 1px solid #ccc;
        margin: 20px 0;
        padding: 10px;
      }
      .future {
        width: 100%;
        height: auto;
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-around;

        .box {
          height: auto;
          border: 1px solid #ccc;
          display: flex;
          flex-direction: column;

          .zt {
            padding-top: 16px;
            padding-bottom: 16px;
          }
        }
      }
    }

    .choose {
      width: 100%;
      height: auto;
      display: flex;
      justify-content: space-between;
      
      >input {
        width: 200px;
        height: 30px;
      }
    }
  }
}
</style>
