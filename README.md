# 项目介绍
蓝鲸产品体系内，一直以来缺少可视化报表能力，导致有视图浏览和配置需求的用户不得不通过外部产品来实现。除此之外，蓝鲸的许多SaaS也有页面上展示可视化视图能力的需求，如果每个产品都自行开发，则会造成人力损耗，体验方面也难以统一。
蓝鲸图表平台则可以解决这些痛点，不仅提供直观的页面级可视化配置能力，也能够将已配置的图表和仪表盘分享嵌入至其他蓝鲸SaaS中。

# SDK属性
| 参数 | 说明                                                                                                          | 类型      | 默认值                |
|------|-------------------------------------------------------------------------------------------------------------|---------|--------------------|
| uid | 分享面板share_uid                                                                                               | String  | ''                 |
| apiPrefix | sdk内ajax请求 api 前缀，比如请求mysql 数据，/api/v1/datasource/query/,:api-prefix ='a',则请求地址为：a/api/v1/datasource/query/ | String  | ''                 |
| timeRange | 面板筛选变量默认时间范围                                                                                                | Array   | ['now/d', 'now/d'] |
| filter | 面板筛选变量，{name:1,name2:2}，                                                                                    | Object  | {}                 |
| waterMark | 水印内容                                                                                                        | Object  | null               |
| isFullScroll | 默认面板将100%充满容器，工具栏固定，此值为false，整个面板将会在容器内滚动                                                                   | Boolean  | true               |
| isShowTools | 是否展示面板上的工具栏，值为false是，工具栏将不展示，工具栏的工具展示属性（如：）配置无效                                                             | Boolean  | true               |
| isShowRefresh | 是否展示面板上的工具栏，值为false是，工具栏将不展示，工具栏的工具展示属性（如：）配置无效                                                             | Boolean  | true               |
| isShowTimeRange | 是否展示时间查询组件                                                                                                  | Boolean  | true               |



# SDK 使用说明
bk-vision 分别支持vue 组件迁入与 纯js引入
+ 纯js-sdk[bk-vision-app](https://git.woa.com/bkvision/bk-vision-app)
+ 以及vue组件sdk[bk-vision-vue](https://git.woa.com/bkvision/bk-vision-vue).


## bk-vision-app
纯js-sdk使用。如果vue项目,推荐使用[bk-vision-vue](https://git.woa.com/bkvision/bk-vision-vue


### 在html文件中引入
```html
  <link rel='stylesheet' href='https://staticfile.qq.com/bkvision/p0964a9106c32428b99e3260d0fc63088/latest/main.css'>
  <script src='https://staticfile.qq.com/bkvision/p0964a9106c32428b99e3260d0fc63088/latest/main.js'/>
  <div id='bkVision' style='width: 100%;height: 500px;'></div>   
  <script>
    window.BkVisionSDK.init(
        '#bkVision', 
      '3asJvRctYHb8YMAEpdQz6W',
      {
        filter: {},
        isShowTools: true,
        waterMark: {
          content: "bk-vision",
        },
        isFullScroll: false,
        isShowRefresh: true,
        isShowTimeRange: true,
        timeRange: ['now/d', 'now/d'],
        apiPrefix: string,
      });
  </script>
```
### 在项目中使用（[暂未发布，请参考内部版@tencent/bk-vision-app](#内部版使用))
```javascript
import 'bk-vision-app'
import 'bk-vision-app/dist/main.css'
window.BkVisionSDK.init('#bkVision', '3asJvRctYHb8YMAEpdQz6W',{apiPrefix:''});
```
### 在vue项目中使用
```vue
<template>
  <div style='width: 100%;height:500px;'>
    <div id='dashboard'/>
  </div>
</template>

<script>
import '@tencent/bk-vision-app'
import '@tencent/bk-vision-app/dist/main.css'
export default {
  name: 'Sdk',
  mounted() {
    window.BkVisionSDK.init('#dashboard', 'TKWQ7s8Uoi2MzY5X6QZkim', {
      filter: {},
      isShowTools: true,
      waterMark: {
        content: "bk-vision",
      },
      isFullScroll: false,
      isShowRefresh: true,
      isShowTimeRange: true,
      timeRange: ['now/d', 'now/d'],
      apiPrefix: string,
    });
  }
};
</script>


```
### 内部版使用
内部版为 **@tencent/bk-vision-app**

#### @tencent/bk-vision-app 安装
参考
```shell
tnpm i @tencent/bk-vision-app
```
更多参看  https://iwiki.woa.com/pages/viewpage.action?pageId=113585381
#### 内部版使用
只是报名增加 **@tencent/**
```javascript
import '@tencent/bk-vision-app'
import '@tencent/bk-vision-app/dist/main.css'
window.BkVisionSDK.init(
  '#bkVision',
  '3asJvRctYHb8YMAEpdQz6W',
  {
    filter: {},
    isShowTools: true,
    waterMark: {
      content: "bk-vision",
    },
    isFullScroll: false,
    isShowRefresh: true,
    isShowTimeRange: true,
    timeRange: ['now/d', 'now/d'],
    apiPrefix: string,
  });
```
#### tnpm无法安装，可以使用git引用
```json
{
  "dependencies": {
    "@tencent/bk-vision-app": "git+https://git.woa.com/bkvision/bk-vision-app",
  }
}
```
## init 函数参数
```typescript
export  function init(
  domId: string, // 需要嵌入的元素的dom id
  uid: string,// 分享uid
  data?: {// 分享面板控制参数
    filter: object,
    isShowTools: boolean,
    waterMark: boolean,
    isFullScroll: boolean,
    isShowRefresh: boolean,
    isShowTimeRange: boolean,
    timeRange: boolean,
    apiPrefix: string,
  },
){}
```

### bk-vision-vue 查询时间默认值说明 {page=#/timeRange}
+ 日期类型：['YYYY-MM-DD HH:mm:ss', 'YYYY-MM-DD HH:mm:ss'],
+ time-shorts：['now-5m', 'now']
####SHORTCUTS 说明
```typescript
/** 时间区间快捷选项 */
export const SHORTCUTS = [
  {
    text: '近5分钟',
    value: ['now-5m', 'now'],
    data: { n: -5, unit: 'm' },
  },
  {
    text: '近15分钟',
    value: ['now-15m', 'now'],
    data: { n: -15, unit: 'm' },
  },
  {
    text: '近30分钟',
    value: ['now-30m', 'now'],
    data: { n: -30, unit: 'm' },
  },
  {
    text: '近1小时',
    value: ['now-1h', 'now'],
    data: { n: -1, unit: 'h' },
  },
  {
    text: '近3小时',
    value: ['now-3h', 'now'],
    data: { n: -1, unit: 'h' },
  },
  {
    text: '近6小时',
    value: ['now-6h', 'now'],
    data: { n: -6, unit: 'h' },
  },
  {
    text: '近12小时',
    value: ['now-12h', 'now'],
    data: { n: -12, unit: 'h' },
  },
  {
    text: '近24小时',
    value: ['now-24h', 'now'],
    data: { n: -24, unit: 'h' },
  },
  {
    text: '近2天',
    value: ['now-2d', 'now'],
    data: { n: -2, unit: 'd' },
  },
  {
    text: '近7天',
    value: ['now-7d', 'now'],
    data: { n: -7, unit: 'd' },
  },
  {
    text: '近30天',
    value: ['now-30d', 'now'],
    data: { n: -30, unit: 'd' },
  },
  {
    text: '今天',
    value: ['now/d', 'now/d'],
  },
  {
    text: '昨天',
    value: ['now-1d/d', 'now-1d/d'],
  },
  {
    text: '前天',
    value: ['now-2d/d', 'now-2d/d'],
  },
  {
    text: '本周',
    value: ['now/w', 'now/w'],
  },
];

```
## 水印属性
具体参看：https://github.com/CoderMonkie/js-watermarker
### options properties <a id="options"></a>

| 属性名 Property 属性                 | 说明 Note 　説明       | 类型 Type タイプ・型 | 是否必须　 Required 　必須 | 可选值 Values 設定値 | 默认值 Default デフォルト値 |
| ------------------------------------ | ---------------------- | -------------------- | -------------------------- | -------------------- | --------------------------- |
| content                              | 水印文字内容           | String / Array       | Required                   |                      |                             |
|                                      |                        |                      |                            |                      |

#### textStyle properties <a id="textStyle"></a>

| 属性名 Property 属性 | 说明 Note 　説明                                                                                            | 类型 Type タイプ・型 | 是否必须　 Required 　必須 | 可选值 Values 設定値 | 默认值 Default デフォルト値                                                                        |
| -------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------- | -------------------------- | -------------------- | -------------------------------------------------------------------------------------------------- |
| left                 | 水印文字的起始横坐标                                                                                        | Integer              | Optional                   |                      | 20                                                                                                 |
| top                  | 水印文字的起始纵坐标<br/>当文字倾斜致显示切字时适当增大该值                                                 | Integer              | Optional                   |                      | 20                                                                                                 |
| color                | 水印文字的颜色<br/>当颜色使用`rgba`时已含透明度故无需`单独的透明度`设置(默认为 1)，如果同时设置将同时起作用 | String               | Optional                   |                      | rgba(150, 150, 150, .15)                                                                           |
| alpha                | 单独设置的透明<br/>若`color`使用了纯色，可单独设置该值控制透明度                                            | Float                | Optional                   |                      | 1                                                                                                  |
| align                | 文字排版                                                                                                    | String               | Optional                   | left/right/center    | left                                                                                               |
| fontFamily           | 字体                                                                                                        | String               | Optional                   |                      | "PingFang SC","Lantinghei SC","Microsoft YaHei",arial,"MS Gothic","\\5b8b\\4f53",sans-serif,tahoma |
| fontSize             | 字号                                                                                                        | Integer              | Optional                   |                      | 16                                                                                                 |
| rotate               | 文字倾斜                                                                                                    | Integer              | Optional                   |                      | 0                                                                                                  |
| lineHeight           | 多行文本时用于累加的行高                                                                                    | Integer              | Optional                   |                      | 25                                                                                                 |
|                      |                                                                                                             |                      |                            |                      |

#### imageStyle properties <a id="imageStyle"></a>

| 属性名 Property 属性 | 说明 Note 　説明 | 类型 Type タイプ・型 | 是否必须　 Required 　必須 | 可选值 Values 設定値         | 默认值 Default デフォルト値 |
| -------------------- | ---------------- | -------------------- | -------------------------- | ---------------------------- | --------------------------- |
| width                | 水印图片宽度     | Integer              | Optional                   |                              | 200                         |
| height               | 水印图片高度     | Integer              | Optional                   |                              | 200                         |
| position             | 水印图片排版     | String               | Optional                   | "x y" (x y：left/top/center) | "left top"                  |
| repeat               | 水印图片重复     | String               | Optional                   | repeat / no-repeat           | repeat                      |
|                      |                  |                      |                            |                              |

---

