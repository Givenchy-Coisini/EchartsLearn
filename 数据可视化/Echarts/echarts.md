## 数据可视化Echarts使用

- 可视化面板布局适配屏幕
- 利用echarts实现柱状图展示

![image-20200811010515187](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200811010515187.png)

**![image-20200811010614537](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200811010614537.png)**

### 什么是数据可视化？

- 目的：借助于图形化的手段，清晰有效的传达于沟通信息
- 数据可视化可以把数据从冰冷的数字转化成图形，揭示蕴含在数据中的规律和道理

### 01-使用技术

完成该项目需要具备以下知识

- div+css布局
- flex布局
- less
- 原生js+jq
- rem适配
- echarts基础

### 02-案例适配方案

- 设计稿是1920px

1. flexible.js 把屏幕分为 24 等份

2. cssrem 插件的基准值是 80px

   插件-配置按钮---配置扩展设置--Root Font Size 里面 设置。

   但是别忘记重启vscode软件保证生效

3. easyless 设置成转化为 css

```json
"less.compile":{
"outExt":".css"
}
```

### 03-基础设置

- body设置背景，缩放为100%，行高1.15
- css初始化

### 04-header布局

- 高度为100px
- 背景图在容器内显示
- 缩放比例为100%
- h1标题部分，白色，38px 居中显示，行高为80px
- 时间模块 ，showTime 定位右侧，right 为30px 行高为75px 文字颜色为：rgba（255，55，55，0.7） 而文字大小为 20px

```js
// 格式： 当前时间：2020年3月17-0时54分14秒
<script>
            var t = null;
            t = setTimeout(time, 1000);//开始运行
            function time() {
                clearTimeout(t);//清除定时器
                dt = new Date();
                var y = dt.getFullYear();
                var mt = dt.getMonth() + 1;
                var day = dt.getDate();
                var h = dt.getHours();//获取时
                var m = dt.getMinutes();//获取分
                var s = dt.getSeconds();//获取秒
                document.querySelector(".showTime").innerHTML = '当前时间：' + y + "年" + mt + "月" + day + "-" + h + "时" + m + "分" + s + "秒";
                t = setTimeout(time, 1000); //设定定时器，循环运行     
            }
 </script>
```

- header部分css样式

```less
header {
  position: relative;
  height: 1.25rem;
  background: url(../images/head_bg.png) no-repeat top center;
  background-size: 100% 100%;
  h1 {
    font-size: 0.475rem;
    color: #fff;
    text-align: center;
    line-height: 1rem;
  }
  .showTime {
    position: absolute;
    top: 0;
    right: 0.375rem;
    line-height: 0.9375rem;
    font-size: 0.25rem;
    color: rgba(255, 255, 255, 0.7);
  }
}
```

### 05-主体部分

- 需要一个上左右的10px 内边距
- column 列容器，分3列 3：5：3

css样式

```css
.mainbox {
  padding: 0.125rem 0.125rem 0;
  display: flex;
  .column {
    flex: 3;
  }
  &:nth-child(2) {
    flex: 5;
  }
}
```

### 06-公共面板模块panel

- 高度为310px
- 1像素的1px solid rgba(25,186,139,0.17)边框
- 有line.jpg背景图片
- padding为上为0 左右15px  下为40px
- 下外边框为15px
- 利用panel 盒子before和after 制作上面两个角，大小为10px，线条为2px solid #02a6b5
- 新加一个盒子 before和after 制作下侧两个角 宽度高度为10px

css样式

```css
.panel {
  position: relative;
  height: 3.875rem;
  border: 1px solid rgba(25, 186, 139, 0.17);
  background: url(../images/line\(1\).png);
  padding: 0 0.1875rem 0.5rem;
  margin-bottom: 0.1875rem;
  &::before {
    position: absolute;
    top: 0;
    left: 0;
    content: "";
    width: 10px;
    height: 10px;
    border-top: 2px solid #02a6b5;
    border-left: 2px solid #02a6b5;
  }
  &::after {
    position: absolute;
    top: 0;
    right: 0;
    content: "";
    width: 10px;
    height: 10px;
    border-top: 2px solid #02a6b5;
    border-right: 2px solid #02a6b5;
  }
  .panel-footer {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    &::before {
      position: absolute;
      bottom: 0;
      left: 0;
      content: "";
      width: 10px;
      height: 10px;
      border-bottom: 2px solid #02a6b5;
      border-left: 2px solid #02a6b5;
    }
    &::after {
      position: absolute;
      bottom: 0;
      right: 0;
      content: "";
      width: 10px;
      height: 10px;
      border-bottom: 2px solid #02a6b5;
      border-right: 2px solid #02a6b5;
    }
  }
}
```

### 07-柱形图bar模块(布局)

- 标题模块： h2 高度为48px 文字颜色为白色，字体大小为20px
- 图表内容模块 chart 高度240px
- 以上可以作为panel公共样式的部分

```css
  h2 {
    height: 0.6rem;
    line-height: 0.6rem;
    text-align: center;
    color: #fff;
    font-size: 20px;
    font-weight: 400;
  }
  .chart {
    height: 3rem;
    background-color: pink;
  }
```

### 08-中间布局

- 上面是no数字模块
- 下面是map地图模块
  - 数字模块.no 有个背景颜色 rgba(101,132,226,0.1);有个15像素的内边距
  - 注意中间列column有个左右10px 下15px 的外边距
  - no模块里面上下划分 上面是数字（no-hd） 下面是相关文字说明（no-hd）
  - no-hd 数字模块 有一个边框 1px solid rgba（25，86，39，0.17）
  - no-hd数字模块里面分为两个小li  每个小li 高度为80px 文字大小为70px 颜色为#ffeb7b 字体是图标字体 electronicFont
  - no-hd利用after 和 before 制作两个小角 边框2px solid #02a6b5 宽度为30px 高度为10px
  - 小竖线 给第一个小li after就可以  1px宽 背景颜色为rgba(255，255，255，0.2) 高度50% top25%即可
  - no-bd 里面也有两个小li 高度为40px 文字颜色为rgba(255,255,255,0.7) 文字大小为18px  上内边距为10px

```css
/* 声明字体*/
@font-face {
  font-family: electronicFont;
  src: url(../font/DS-DIGIT.TTF);
}
```

map

- 地图模块高度为810px 里面包含4个盒子 chart放图表模块 球体盒子 旋转1 旋转2
- 球体图片模块 map1 大小为518px 要加背景图片 因为要缩放100% 定位到最中央 透明度为0.3
- 旋转1 map2 大小为643px 要加背景图片 因为要缩放100% 定位到中央 透明度为0.6 做旋转动画 利用z-index压住球体
- 旋转2 map3 大小为586 也要加背景图片 因为要缩放100% 定位到中央  做旋转动画（逆时针）

```html
<div class="no">
                <div class="no-hd">
                    <ul>
                        <li>125811</li>
                        <li>104563</li>
                    </ul>
                </div>
                <div class="no-bd">
                    <ul>
                        <li>前端需求人数</li>
                        <li>市场供应人数</li>
                    </ul>
                </div>
            </div>
            <div class="map">
                <div class="chart"></div>
                <div class="map1"></div>
                <div class="map2"></div>
                <div class="map3"></div>
            </div>
```

中间样式

```css
/* 声明字体*/
@font-face {
  font-family: electronicFont;
  src: url(../font/DS-DIGIT.TTF);
}
.no {
  background: rgba(101, 132, 226, 0.1);
  padding: 0.1875rem;
  .no-hd {
    position: relative;
    border: 1px solid rgba(25, 186, 139, 0.17);
    &::before {
      content: "";
      position: absolute;
      width: 30px;
      height: 10px;
      border-top: 2px solid #02a6b5;
      border-left: 2px solid #02a6b5;
      top: 0;
      left: 0;
    }
    &::after {
      content: "";
      position: absolute;
      width: 30px;
      height: 10px;
      border-bottom: 2px solid #02a6b5;
      border-right: 2px solid #02a6b5;
      right: 0;
      bottom: 0;
    }
    ul {
      display: flex;
      li {
        position: relative;
        flex: 1;
        text-align: center;
        height: 1rem;
        line-height: 1rem;
        font-size: 0.875rem;
        color: #ffeb7b;
        padding: 0.05rem 0;
        font-family: electronicFont;
        font-weight: bold;
        &:first-child::after {
          content: "";
          position: absolute;
          height: 50%;
          width: 1px;
          background: rgba(255, 255, 255, 0.2);
          right: 0;
          top: 25%;
        }
      }
    }
  }
  .no-bd ul {
    display: flex;
    li {
      flex: 1;
      height: 0.5rem;
      line-height: 0.5rem;
      text-align: center;
      font-size: 0.225rem;
      color: rgba(255, 255, 255, 0.7);
      padding-top: 0.125rem;
    }
  }
}
.map {
  position: relative;
  height: 10.125rem;
  .chart {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 5;
    height: 10.125rem;
    width: 100%;
  }
  .map1,
  .map2,
  .map3 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 6.475rem;
    height: 6.475rem;
    background: url(../images/map.png) no-repeat;
    background-size: 100% 100%;
    opacity: 0.3;
  }
  .map2 {
    width: 8.0375rem;
    height: 8.0375rem;
    background-image: url(../images/lbx.png);
    opacity: 0.6;
    animation: rotate 15s linear infinite;
    z-index: 2;
  }
  .map3 {
    width: 7.075rem;
    height: 7.075rem;
    background-image: url(../images/jt.png);
    animation: rotate1 10s linear infinite;
  }

  @keyframes rotate {//css3动画
    from {
      transform: translate(-50%, -50%) rotate(0deg);
    }
    to {
      transform: translate(-50%, -50%) rotate(360deg);
    }
  }
  @keyframes rotate1 {
    from {
      transform: translate(-50%, -50%) rotate(0deg);
    }
    to {
      transform: translate(-50%, -50%) rotate(-360deg);
    }
  }
}

```

### 09-Echarts介绍

常见的数据可视化库

- D3.js 目前web端评价最高的js可视化工具库（入手难）
- ECharts 百度出品的一个开源js数据可视化库
- Highcharts.js 国外的前端数据可视化库，非常用免费 被国外很多大公司所用
- AbtV 蚂蚁金服全新一代数据可视化解决方案
- Highcharts和Echarts就像office和wps的关系一样

> Echarts，一个使用js实现的可视化开源库，可以流畅的运行在pc和移动端上，兼容当前绝大部分浏览器，底层依赖矢量图形库ZRender，提供直观，丰富交互，可高度个性化定制的数据可视化图标库

大白话：

- 是一个js插件
- 性能好可流畅运行pc与移动端
- 兼容祝融浏览器
- 提高跟多常用图标，且可定制
  -  折线图、柱状图、散点图、饼图、K线图

官网地址：https://www.echartsis.com/zh/index.html

### 10-Echarts 体验

官方教程：

[五分钟上手Echarts]: https://echarts.apache.org/zh/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts

- 下载echarts：https://echarts.apache.org/zh/download.html

使用步骤：

![image-20200811164302446](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200811164302446.png)

- 引入echarts插件文件到html页面中
- 准备一个具备大小的DOM容器

```html
<div id="main" style="width: 600px;height:400px;"></div>
```

- 初始化echarts实例对象

```html
var myChart = echarts.init(document.getElementById('main'));
```

- 指定配置项和数据

```js
var option = {
    xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    },
    yAxis: {
        type: 'value'
    },
    series: [{
        data: [820, 932, 901, 934, 1290, 1330, 1320],
        type: 'line'
    }]
};
```

- 将配置项设置给echarts实例对象

```html
myChart.setOption(option);
```

### 11-echarts基础配置

> 需要了解的主要配置：`series`、`xAxis`、`yAxis`、`grid`、`tooltip`、`title`、`legend`、`color`

- `series`:
  - 系列列表。每个系列通过 `type` 决定自己的图表类型 柱形还是折线
  - 大白话：图标数据，指定什么类型的图标，可以多个图表重叠。
  - 数据堆叠，同个类目轴上系列配置相同的`stack`值后 后一个系列的值会在前一个系列的值上相加。
- `title`:标题组件
- `tooltip`：图标的提示框组件
  - `trigger`触发方式 ：坐标 数据项触发 等等
- `legend`：图例组件  //series有了name值 这个可以删掉
- `toolbox`:工具箱组件 可以另存为图片等功能
- `grid`：网格配置--->可以控制图表大小

```js
grid:{
left:"3%",//距离dom容器左侧距离
right:"4%",//右侧
bottom:"3%",
  //是否显示刻度标签，如果是true 就显示，如果是false 就不显示
containLabel:true
}
```

- `xAxis`:设置x轴的相关配置：type：“category"类目  value：数字
  - boundaryGap 是否让我们的线条和坐标轴有缝隙
  - data：x轴的下面的字

- `color`：调色

```js
option = {
    // color设置我们线条的颜色 注意后面是个数组
    color: ['pink', 'red', 'green', 'skyblue'],
    // 设置图表的标题
    title: {
        text: '折线图堆叠123'
    },
    // 图表的提示框组件 
    tooltip: {
        // 触发方式
        trigger: 'axis'
    },
    // 图例组件
    legend: {
       // series里面有了 name值则 legend里面的data可以删掉
    },
    // 网格配置  grid可以控制线形图 柱状图 图表大小
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        // 是否显示刻度标签 如果是true 就显示 否则反之
        containLabel: true
    },
    // 工具箱组件  可以另存为图片等功能
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    // 设置x轴的相关配置
    xAxis: {
        type: 'category',
        // 是否让我们的线条和坐标轴有缝隙
        boundaryGap: false,
        data: ['星期一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
     // 设置y轴的相关配置
    yAxis: {
        type: 'value'
    },
    // 系列图表配置 它决定着显示那种类型的图表
    series: [
        {
            name: '邮件营销',
            type: 'line',
           
            data: [120, 132, 101, 134, 90, 230, 210]
        },
        {
            name: '联盟广告',
            type: 'line',

            data: [220, 182, 191, 234, 290, 330, 310]
        },
        {
            name: '视频广告',
            type: 'line',
          
            data: [150, 232, 201, 154, 190, 330, 410]
        },
        {
            name: '直接访问',
            type: 'line',
          
            data: [320, 332, 301, 334, 390, 330, 320]
        }
    ]
};
```

### 12-柱状图图标(两大步骤)

- 官网找到类似实例，适当分析，并且引入到html页面中
- 根据需求定制图表

1.引入到html页面中

```js
//! 柱状图模块1
(function(){
    // fyj 1.实例化对象
    var myChart = echarts.init(document.querySelector(".bar .chart"));
    // 指定配置项和数据
    var option = {
        color: ['#3398DB'],
        tooltip: {
            trigger: 'axis',
            axisPointer: {            // 坐标轴指示器，坐标轴触发有效
                type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
            }
        },
        grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
        },
        xAxis: [
            {
                type: 'category',
                data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                axisTick: {
                    alignWithLabel: true
                }
            }
        ],
        yAxis: [
            {
                type: 'value'
            }
        ],
        series: [
            {
                name: '直接访问',
                type: 'bar',
                barWidth: '60%',
                data: [10, 52, 200, 334, 390, 330, 220]
            }
        ]
    };
    // 3.把配置项给实例对象
    myChart.setOption(option)
})();
```

2.根据需求定制图表

- 修改图表柱形颜色 #2f89cf
- 修改图表大小  top为10px  bottom为4% grid决定我们图表的大小

```js
  color: ['#2f89cf'],
  grid: {
            left: '0%',
            top:'10px',
            right: '0%',
            bottom: '4%',
            containLabel: true
      },
```

- x轴相关设置 xAxis
  -  文本颜色设置为 rgba（255，255，255，.6） 字体大小为12px
  - x轴线的样式不显示

```js
// x轴的文字颜色和大小 
axisLabel: { 
color: "rgba(255,255,255,.6)", fontSize: "12" },
// x轴样式不显示
axisLine: { 
show: false 
  // 如果想要设置单独的线条样式 
lineStyle: { 
  color: "rgba(255,255,255,.1)", 
    width: 1,  
    type: "solid" }
}
```

- Y轴相关设置
  - 文本颜色设置为 rgba（255，255，255，.6） 字体大小为12px
  - y轴线条样式更改为1像素的rgba(255,255,255,.1)边框
  - 分割线的颜色修饰为1像素的rgba(255，255，255，.1)

```js
// y 轴文字标签样式
axisLabel: {
      color: "rgba(255,255,255,.6)",
       fontSize: "12"
},
 // y轴线条样式
 axisLine: {
      lineStyle: {
         color: "rgba(255,255,255,.1)",
         // width: 1,
         // type: "solid"
      }
5232},
 // y 轴分隔线样式
splitLine: {
    lineStyle: {
       color: "rgba(255,255,255,.1)"
     }
}
```

- 修改柱形为圆角以及柱子宽度series里面设置

```js
series: [
            {
                name: '直接访问',
                type: 'bar',
                barWidth: '35%',
                data: [10, 52, 200, 334, 390, 330, 220],
                itemStyle:{
                    // todo 修改柱子的颜色
                    barBorderRadius:5
                }
            }
        ]
```

- 更换对应的数据

```js
// x轴中更换data数据
 data: [ "旅游行业","教育培训", "游戏行业", "医疗行业", "电商行业", "社交行业", "金融行业" ],
// series 更换数据
 data: [200, 300, 300, 900, 1500, 1200, 600]
```

- 让图标跟随屏幕自适应

```js
window.addEventListener("resize",function(){
        myChart.resize();
   })
```

### 13-柱形图2定制

- 官网找到类似实例，对应分析，并且引入到html页面中
- 根据需求定制图表

需求1：修改图形大小 grid

```js
 grid: {
            left: '22%',
            top:'10%',
            bottom: '10%',
            containLabel: true
        },
```

需求2：不需要显示x轴信息

```js
 xAxis: {
            show:false
      },
```

需求3：不显示y轴线和相关刻度

```js
      axisLine:{
                show:false
            },
            axisTick:{
                show:false
            },
```

需求4：y轴的文字颜色改为白色

```js
axisLabel: { 
color: ”#fff“ },
```

需求5：修改第一组柱子的相关样式（条状）

```js
name: "条",
// 柱子之间的距离
barCategoryGap: 50,
//柱子的宽度
barWidth: 10,
// 柱子设为圆角
itemStyle: {
    normal: {
      barBorderRadius: 20,       
    }
},
```

- 设置第一组柱子内百分比显示数据

```js
label:{
                    show:true,
                    position:"inside",
                    formatter:"{c}%"//data中的数据
                }
```

- 设置第一组柱子的不同颜色

```js
// 声明颜色数组
var myColor = ["#1089E7", "#F57474", "#56D0E3", "#F8B448", "#8B78F6"];
// 2. 给 itemStyle  里面的color 属性设置一个 返回值函数
  itemStyle: {
          normal: {
            barBorderRadius: 20,  
            // params 传进来的是柱子对象
            console.log(params);
            // dataIndex 是当前柱子的索引号
            return myColor[params.dataIndex];
          }
         
},
```

需求6：修改第二组柱子的相关配置（框状）

```js
 name: '框',
                type: 'bar',
                data: [35, 50, 70, 30, 20],
                // todo 柱子之间的间距
                barCategoryGap:50,
                // 柱子的宽度
                barWidth:15,
                // todo 修改第一组柱子的圆角
                itemStyle:{
                    normal:{
                        color:'none',
                        borderColor:'#00c1de',
                        borderWidth:3,
                        barBorderRadius:15,
                    // 此时的color可以修改柱子的颜色
                    }
                },               
```

- 给y轴添加第二组数据

```js
yAxis: [
      {
      type: "category",
      data: ["印尼", "美国", "印度", "中国", "世界人口(万)"],
      // 不显示y轴的线
      axisLine: {
        show: false
      },
      // 不显示刻度
      axisTick: {
        show: false
      },
      // 把刻度标签里面的文字颜色设置为白色
      axisLabel: {
        color: "#fff"
      }
    },
      {
        show: true,
        data: [702, 350, 610, 793, 664],
           // 不显示y轴的线
      axisLine: {
        show: false
      },
      // 不显示刻度
      axisTick: {
        show: false
      },
        axisLabel: {
          textStyle: {
            fontSize: 12,
            color: "#fff"
          }
        }
      }
    ],
```

需求6：设置两组柱子层叠以及更换数据

```js
// 给series  第一个对象里面的 添加 
yAxisIndex: 0,
// 给series  第二个对象里面的 添加 
yAxisIndex: 1,
// series 第一个对象里面的data
data: [70, 34, 60, 78, 69],
// series 第二个对象里面的data
data: [100, 100, 100, 100, 100],
// y轴更换第一个对象更换data数据
data: ["HTML5", "CSS3", "javascript", "VUE", "NODE"],
// y轴更换第二个对象更换data数据
data:[702, 350, 610, 793, 664],
```

### 14-折线图：人员变化模块的制作

- 官网找到类似实例，对应分析，并且引入到html页面中
- 根据需求定制图表

需求1：修改折线图大小，显示边框颜色设置为 #012f4a 并且显示刻度标签

```js
grid: {
            left: '3%',
            top:'20%',
            right: '4%',
            bottom: '3%',
            show:true,//显示边框
            borderColor:'#012f4a',
            containLabel: true
        },
```

需求2：修改图例组件中的文字颜色  #4c9bfd 距离右侧right为10%

```js
 legend: {
            data: ['邮件营销', '联盟广告'],
            textStyle:{
                color:'#4c9bfd'//图例文字颜色
            },
            right:"10%"
        },
```

需求3：x轴相关配置

- 刻度去除
- x轴刻度标签字体颜色：#4c9bfd
- 剔除坐标轴颜色（将来使用y轴分割线）
- 轴两端是不需要内边距的 boundaryGap

```js
xAxis: {
            type: 'category',
            boundaryGap: false,
            data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
            axisTick:{//去除刻度线
                show:false,
            },
            axisLabel:{
                color:'#4c9bfd'
            },
            axisLine:{
                show:false//去除轴线
            }
        },
```

需求4：y轴相关配置

- 刻度去除
- 字体颜色：#4c9bfd
- 分割线颜色：#012f4a

```js
 yAxis: {
            type: 'value',
            axisTick:{//去除刻度线
                show:false,
            },
            axisLabel:{//修改文字、刻度标签颜色
                color:'#4c9bfd'
            },
            axisLine:{
                show:false//去除轴线
            },
            splitLine:{
                lineStyle: {
                    color: 'rgba(255,255,255,.1)'
                }
            }
        },
```

需求5：两条线形图定制

- 颜色为 #00f2f1 #ed3f35

- 把折线修饰为圆滑 series数据中添加smooth为true

  ```js
   smooth:true,
   color:['#00f2f1','#ed3f35'],
  ```

需求6：配置数据

```js
// x轴的文字
xAxis: {
  type: 'category',
  data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
```

```js
// 图标数据
    series: [{
      name:'新增粉丝',
      data:  [24, 40, 101, 134, 90, 230, 210, 230, 120, 230, 210, 120],
      type: 'line',
      smooth: true
    },{
      name:'新增游客',
      data: [40, 64, 191, 324, 290, 330, 310, 213, 180, 200, 180, 79],     
      type: 'line',
      smooth: true
      }
    }]
```

需求7： 新增需求 点击 2020年 2021年 数据发生变化

以下是后台送过来数据（ajax请求过来的）

```js
 var yearData = [
      {
        year: '2020',  // 年份
        data: [  // 两个数组是因为有两条线
             [24, 40, 101, 134, 90, 230, 210, 230, 120, 230, 210, 120],//拿到后台数据以后 就给series中的data赋值
             [40, 64, 191, 324, 290, 330, 310, 213, 180, 200, 180, 79]
          ]
      },
      {
        year: '2021',  // 年份
        data: [  // 两个数组是因为有两条线
             [123, 175, 112, 197, 121, 67, 98, 21, 43, 64, 76, 38],
     		[143, 131, 165, 123, 178, 21, 82, 64, 43, 60, 19, 34]
          ]
      }
     ];
```

- tab栏切换事件
- 点击2020按钮 需要把 series 第一个对象里面的data 换成 2020年对象里面data[0]
- 点击2020按钮 需要把 series 第二个对象里面的data 换成 2020年对象里面data[1]
- 2021 按钮同样道理

### 15-折线图2播放量模块制作

- 官网找到类似实例，适当分析，并且引入到html页面中
- 根据需求定制图表

需求1：更换图例组件文字颜色 rgba(255,255,255..5)文字大小为12

```js
legend: {
           top:'0%',
            data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎'],
            textStyle: {
                    color: '#rgba(255,255,255,.5)'//图例文字颜色
            },
            fontSize:"12"
      },
```

需求2：修改图表的大小

```js
     grid: {
            top: '30',
            left: '10',
            right: '10',
            bottom: '10',
            containLabel: true
        },
```

需求3：修改x轴相关配置

- 修改文本颜色为rgba(255,255,255,.6) 文字大小为 12
- x轴线的颜色为 rgba(255,255,255,.2)

```js
  axisLabel: {
                    color: 'rgba(255,255,255,.6)',
                    fontSize: "12"
                },
                //fyj不显示x轴的样式
                axisLine: {
                   lineStyle:{
                       color:"rgba(255,255,255,.2)"
                   }
                }
```

需求4：修改y轴的相关配置

```js
     axisTick: { show: false },//刻度
        axisLine: {
          lineStyle: {
            color: "rgba(255,255,255,.1)"
          }
        },
        axisLabel: {
          textStyle: {
            color: "rgba(255,255,255,.6)",
            fontSize: 12
          }
        },
	   // 修改分割线的颜色
        splitLine: {
          lineStyle: {
            color: "rgba(255,255,255,.1)"
          }
        }
      
```

需求5：修改两个线模块配置

```js
  //第一条 线是圆滑
       smooth: true,
        // 单独修改线的样式
        lineStyle: {
            color: "#0184d5",
            width: 2 
        },
         // 填充区域
        areaStyle: {
              // 渐变色，只需要复制即可
            color: new echarts.graphic.LinearGradient(
              0,
              0,
              0,
              1,
              [
                {
                  offset: 0,
                  color: "rgba(1, 132, 213, 0.4)"   // 渐变色的起始颜色
                },
                {
                  offset: 0.8,
                  color: "rgba(1, 132, 213, 0.1)"   // 渐变线的结束颜色
                }
              ],
              false
            ),
            shadowColor: "rgba(0, 0, 0, 0.1)"
        },
        // 设置拐点 小圆点
        symbol: "circle",
        // 拐点大小
        symbolSize: 8,
        // 设置拐点颜色以及边框
       itemStyle: {
            color: "#0184d5",
            borderColor: "rgba(221, 220, 107, .1)",
            borderWidth: 12
        },
        // 开始不显示拐点， 鼠标经过显示
        showSymbol: false,
```

```js
  name: "转发量",
        type: "line",
        smooth: true,
        lineStyle: {
          normal: {
            color: "#00d887",
            width: 2
          }
         },
         areaStyle: {
          normal: {
            color: new echarts.graphic.LinearGradient(
              0,
              0,
              0,
              1,
              [
                {
                  offset: 0,
                  color: "rgba(0, 216, 135, 0.4)"
                },
                {
                  offset: 0.8,
                  color: "rgba(0, 216, 135, 0.1)"
                }
              ],
              false
            ),
            shadowColor: "rgba(0, 0, 0, 0.1)"
          }
        },
        // 设置拐点 小圆点
        symbol: "circle",
        // 拐点大小
        symbolSize: 5,
        // 设置拐点颜色以及边框
         itemStyle: {
            color: "#00d887",
            borderColor: "rgba(221, 220, 107, .1)",
            borderWidth: 12
        },
        // 开始不显示拐点， 鼠标经过显示
        showSymbol: false,
```

需求6：更换数据

```js
// x轴更换数据
data: [ "01","02","03","04","05","06","07","08","09","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","26","28","29","30"],
// series  第一个对象data数据
 data: [ 30, 40, 30, 40,30, 40, 30,60,20, 40, 30, 40, 30, 40,30, 40, 30,60,20, 40, 30, 40, 30, 40,30, 40, 20,60,50, 40],
// series  第二个对象data数据
 data: [ 130, 10, 20, 40,30, 40, 80,60,20, 40, 90, 40,20, 140,30, 40, 130,20,20, 40, 80, 70, 30, 40,30, 120, 20,99,50, 20],
```

### 16-饼形图 1年龄分布模块制作

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

定制图表需求1：

- 修改图例组件在底部并且居中显示。
- 每个小图标的宽度和高度修改为 10px
- 文字大小为12 颜色 rgba(255,255,255,.5)

```js
 legend: {
            // 距离底部0%
            bottom:"0%",
            //小图标的宽度和高度
            itemWidth:10,
            itemHeight:10,
            data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎'],
            // todo 修改图例组件的文字为12px
            textStyle:{
                color:"rgba(255,255,255,.5)",
                fontSize:"12"
            }
        },
```

需求2：

- 修改水平居中，垂直居中
- 修改内圆半径和外圆半径为【“40%”，“60%”】 带有直角坐标系的比如折线图柱状图是grid修改图形大小，而我们饼形图是通过radius修饰大小

```js
series: [
      {
        name: "年龄分布",
        type: "pie",
        // 设置饼形图在容器中的位置
        center: ["50%", "50%"],
        //  修改内圆半径和外圆半径为  百分比是相对于容器宽度来说的
        radius: ["40%", "60%"],
        // 不显示标签文字
        label: { show: false },
        // 不显示连接线
        labelLine: { show: false },
      }
    ]
```

需求3：更换数据

```js
// legend 中的data  可省略
data: ["0岁以下", "20-29岁", "30-39岁", "40-49岁", "50岁以上"],
//  series 中的数据
 data: [
          { value: 1, name: "0岁以下" },
          { value: 4, name: "20-29岁" },
          { value: 2, name: "30-39岁" },
          { value: 2, name: "40-49岁" },
          { value: 1, name: "50岁以上" }
 ] ,
```

定制需求4： 更换颜色

```js
color: [
          "#065aab",
          "#066eab",
          "#0682ab",
          "#0696ab",
          "#06a0ab",
        ],
 // 4. 让图表跟随屏幕自动的去适应
  window.addEventListener("resize", function() {
    myChart.resize();
  });
```

### 17-饼形图2 地区分布模块制作（南丁格尔玫瑰图）

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

第二步：按照需求定制

- 需求1：颜色设置

```js
color: ['#006cff', '#60cda0', '#ed8884', '#ff9f7f', '#0096ff', '#9fe6b8', '#32c5e9', '#1d9dff'],
```

- 需求2：修改饼形图大小 ( series对象)

```js
radius: ['10%', '70%'],
```

- 需求3： 把饼形图的显示模式改为 半径模式

```js
 roseType: "radius",
```

- 需求4：数据使用更换（series对象 里面 data对象）

```js
          { value: 20, name: '云南' },
          { value: 26, name: '北京' },
          { value: 24, name: '山东' },
          { value: 25, name: '河北' },
          { value: 20, name: '江苏' },
          { value: 25, name: '浙江' },
          { value: 30, name: '四川' },
          { value: 42, name: '湖北' }
```

- 需求5：字体略小些 10 px ( series对象里面设置 )

  饼图图形上的文本标签可以控制饼形图的文字的一些样式。 label 对象设置

```js
series: [
      {
        name: "面积模式",
        type: "pie",
        radius: [30, 110],
        center: ["50%", "50%"],
        roseType: "radius",
        // 文本标签控制饼形图文字的相关样式， 注意它是一个对象
        label: {
          fontSize: 10
        },
      }
    ]
  };
```

- 需求6：防止缩放的时候，引导线过长。引导线略短些 (series对象里面的 labelLine 对象设置 )
  - 连接图表 6 px
  - 连接文字 8 px

```js
+        // 文字调整
+        label:{
+          fontSize: 10
+        },
+        // 引导线调整
+        labelLine: {
+          // 连接扇形图线长
+          length: 6,
+          // 连接文字线长
+          length2: 8
+        } 
+      }
+    ],
```

- 需求6：浏览器缩放的时候，图表跟着自动适配。

```js
// 监听浏览器缩放，图表对象调用缩放resize函数
window.addEventListener("resize", function() {
    myChart.resize();
  });
```

- 需求7：图例组件

```js
 legend: {
            left: 'center',
            top: 'bottom',
            bottom: "0%",
            //小图标的宽度和高度
            itemWidth: 10,
            itemHeight: 10,
            textStyle: {
                color: "rgba(255,255,255,.5)",
                fontSize: "12"
            }
        },
```

### 18-Echarts-社区介绍

> 社区就是一些，活跃的echarts使用者，交流和贡献制定好的图表的地方

![image-20200812145836386](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200812145836386.png)

- 在这里可以找到一些基于echarts的高度定制好的图表，相当于jq的开发的插件，这里是基于echarts开发的第三方的图表

### 19-echarts-map使用（扩展）

参考社区例子:https://gallery.echartsjs.com/editor.html?c=x0-ExSkZDM(模拟飞机航线)

实现步骤：

- 第一需要下载china.js提供中国地图的js文件
- 第二个因为里面代码比较多，我们新建一个新的js文件 myMap.js 引入
- 使用社区提供的配置即可。

需要修改：

- 去掉标题组件
- 去掉背景颜色
- 修改地图省份背景 #142957 areaColor 里面做修改
- 地图放大通过 zoom 设置为1.2即可

```js
    geo: {
      map: 'china',
      zoom: 1.2,
      label: {
        emphasis: {
          show: false
        }
      },
      roam: false,
      itemStyle: {
        normal: {
          areaColor: '#142957',
          borderColor: '#0692a4'
        },
        emphasis: {
          areaColor: '#0b1c2d'
        }
      }
    },
```

总结：这例子是扩展案例，大家以后可以多看看社区里面的案例。

### 20- 最后约束缩放

```js
/* 约束屏幕尺寸 */
@media screen and (max-width: 1024px) {
  html {
    font-size: 42px !important;
  }
}
@media screen and (min-width: 1920px) {
  html {
    font-size: 80px !important;
  }
}
```

