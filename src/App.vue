<template>
  <div id="nav">
    <div class="chart" id="chart"></div>
    <div class="test">
      <div class="true">
        <img src="./assets/left_black@2x.png" />

      </div>
      <div class="fake">
        <div class="left"></div>
        <div class="canvas">
          <canvas id="canvas" ref="canvas" width="62" height="52"></canvas>

        </div>

      </div>
      <div class="swiper-container">
         <div class="swiper-wrapper">
           <div class="swiper-slide" v-for="(item,index) in 60" :key="index">
           {{index}}
           </div>
         </div>
      </div>
    </div>

  </div>
  <router-view />
</template>
<script >
import { defineComponent, nextTick } from 'vue';
// import _ from 'lodash-es';
import Swiper from 'swiper';
import 'swiper/css/swiper.css';
import * as echarts from 'echarts';
export default defineComponent({

  setup() {
    //  const myCanvas=ref(null)

    //  console.log(canvas.value)
    let swiper=null;

    
    nextTick(() => {
      swiper=new Swiper('.swiper-container',{
          direction:'vertical',
          autoplay:{
            delay:2000,
            disableOnInteraction:false
          },
          itemHeight:100,
          slidesPerView:10,
          slidesPerGroup:10,
          loop:true
    })
      let echart = echarts.init(document.getElementById('chart'))
      echart.setOption({
        title: {
          text: 'Stacked Line'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['Email', 'Union Ads', 'Video Ads', 'Direct', 'Search Engine']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: 'Email',
            type: 'line',
            stack: 'Total',
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: 'Union Ads',
            type: 'line',
            stack: 'Total',
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: 'Video Ads',
            type: 'line',
            stack: 'Total',
            data: [150, 232, 201, 154, 190, 330, 410]
          },
          {
            name: 'Direct',
            type: 'line',
            stack: 'Total',
            data: [320, 332, 301, 334, 390, 330, 320]
          },
          {
            name: 'Search Engine',
            type: 'line',
            stack: 'Total',
            data: [820, 932, 901, 934, 1290, 1330, 1320]
          }
        ]
      })
      echart.on('mouseover', 'series', (params) => {
        console.log(params)
      })
      let ratio = window.devicePixelRatio || 1;

      let canvas = document.getElementById('canvas');
      let context = canvas.getContext('2d');

      canvas.style.width = canvas.width + 'px';
      canvas.style.height = canvas.height + 'px';
      canvas.width = canvas.width * ratio;
      canvas.height = canvas.height * ratio;
      context.scale(ratio, ratio);
      context.beginPath();
      context.strokeStyle = "red";
      context.lineWidth = 1;
      // context.moveTo(0,0);
      context.lineTo(0, 0);
      context.lineTo(10, 0)



      context.stroke();
      context.closePath();



    })
    return {
      // myCanvas
    }
  }
})
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.swiper-container{
  height: 400px;
  width: 500px;
  .swiper-wrapper{
    .swiper-slide{
       height: 100px;
       background: red;

    }
  }
}
.chart {
  width: 300px;
  height: 300px;

}

.swiper-container {
  width: 500px;
  background: #ccc;
  height: 500px;

  .slider-wrapper {
    .swiper-slide {
      height: 50px;
      background: red;
    }
  }
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.test {
  width: 300px;
  // background: #1d1e22;;
  height: 300px;
  padding-top: 10px;

  .true {
    margin: 0 0 2px 10px;

    width: 256px;

    position: relative;

    img {
      // margin: 10px 0 2px;
      display: block;
      width: 256px;
      height: 52px;
      position: relative;

    }

    &::before {
      position: absolute;
      display: block;
      content: ' ';
      top: -0px;
      right: 10px;
      height: 300px;
      background: yellow;
      transform: scaleX(0.5);
      width: 1px;
    }

    &::after {
      position: absolute;
      display: block;
      content: ' ';
      top: -0px;
      right: 42px;
      height: 300px;
      background: blue;
      transform: scaleX(0.5);
      width: 1px;
    }
  }

  .fake {
    position: absolute;
    top: 48px;
    margin-left: 10px;
    width: 256x;
    height: 52px;
    display: flex;

    .left {
      width: 194px;
      height: 52px;
      border: 1px solid red;
      box-sizing: border-box;
      background: #27292d;
      position: relative;

      &::after {
        position: absolute;
        display: block;
        content: ' ';
        // top: -0px;
        bottom: -1px;
        height: 1px;
        background: blue;
        width: 400px;
        display: none;
      }
    }

    .canvas {
      width: 62px;
      height: 52px;
    }
  }
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}

.list-enter,
.list-leave-to

/* .list-leave-active for below version 2.1.8 */
  {
  opacity: 0;
  transform: translateY(30px);
}

/* 下面的 .v-move 和 .v-leave-active 配合使用，能够实现列表后续的元素，渐渐地移动过来的效果 */
.list-move {
  transition: all 0.6s ease;
}

.list-leave-active {
  position: absolute;
}
</style>
