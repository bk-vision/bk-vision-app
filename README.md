# 项目介绍

# SDK 使用说明
bk-vision sdk 分别为纯js-sdk([bk-vision-app](#bk-vision-app))，以及vue组件sdk([bk-vision-vue](#bk-vision-vue)).
## SDK属性
| 参数 | 说明                                                                                                          | 类型      | 默认值 |
|------|-------------------------------------------------------------------------------------------------------------|---------|-----|
| uid | 分享面板share_uid                                                                                               | String  | ''   |
| apiPrefix | sdk内ajax请求 api 前缀，比如请求mysql 数据，/api/v1/datasource/query/,:api-prefix ='a',则请求地址为：a/api/v1/datasource/query/ | String  | ''    |
| timeRange | 面板筛选变量默认时间范围                                                                                                | Array   | ['now/d', 'now/d']   |
| filter | 面板筛选变量，{name:1,name2:2}，                                                                                    | Object  | {}  |
| isFullScroll | 默认面板将100%充满容器，工具栏固定，此值为false，整个面板将会在容器内滚动                                                                               | Boolean  | true  |
| isShowTools | 是否展示面板上的工具栏，值为false是，工具栏将不展示，工具栏的工具展示属性（如：）配置无效                                                                              | Boolean  | true  |
| isShowRefresh | 是否展示面板上的工具栏，值为false是，工具栏将不展示，工具栏的工具展示属性（如：）配置无效                                                                              | Boolean  | true  |
| isShowTimeRange |  是否展示时间查询组件                                                                             | Boolean  | true  |


## bk-vision-app
纯js-sdk使用。如果vue项目,推荐使用[bk-vision-vue](#bk-vision-vue)
https://www.npmjs.com/package/bk-vision-app
### 在项目中使用
```javascript
import 'bk-vision-app'
import 'bk-vision-app/dist/main.css'
window.BkVisionSDK.init('#app', '3asJvRctYHb8YMAEpdQz6W');
```
### 在html文件中引入
```html
<link rel='stylesheet' href='bk-vision-app/dist/main.css'>
  <script src='bk-vision-app/dist/main.js'/>
  <script>
    window.BkVisionSDK.init('#app', '3asJvRctYHb8YMAEpdQz6W', {apiPrefix:''});
  </script>
```
### 在vue项目中使用
```vue
<template>
 <div>
   <div id='dashboard' class="home" style='flex:1;'/>
 </div>
</template>

<script>
import 'bk-vision-app'
import 'bk-vision-app/dist/main.css'
export default {
  name: 'Sdk',
  mounted() {
    window.BkVisionSDK.init('#dashboard', '3asJvRctYHb8YMAEpdQz6W',{apiPrefix:''});
  }
};
</script>

```
###init 函数参数
```typescript
export  function init(
  domId: string,
  uid: string,
  data?: {
    filter: object,
    isShowTools: boolean,
    isShowWaterMark: boolean,
    isFullScroll: boolean,
    isShowRefresh: boolean,
    isShowTimeRange: boolean,
    timeRange: boolean,
    apiPrefix: string,
  },
){}
```
## bk-vision-vue
https://www.npmjs.com/package/bk-vision-vue
## 使用
安装bk-vision
```bash
npm install bk-vision-vue
```
### 项目中使用
```vue
<bk-dashboard 
  :is-show-tools='true' 
  :is-show-refresh='true' 
  :is-show-time-range='true'
  uid='FwchfLZSsoaBSzjpW7WBa7'
  api-prefix="http://127.0.0.1:8001/bkvision/"/>
```

完整案例
```vue
<template>
  <div class="home" style='flex:1;'>
    <bk-dashboard
      :is-show-tools='true'
      :is-show-refresh='true'
      :is-show-time-range='true'
      uid='FwchfLZSsoaBSzjpW7WBa7'
      api-prefix="http://127.0.0.1:8001/bkvision/"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import BkDashboard from 'bk-vision-vue'
import 'bk-vision-vue/dist/main.css'

@Component({
  components: {
    BkDashboard
  }
})
export default class HomeView extends Vue {
}
</script>

```

### bk-vision-vue 组件属性 {page=#/props}
bk-vision-vue 组件属性说明
```typescript
export default Vue.extend({
    name: 'BkDashboard',
    // components: { GridPanel },
    props: {
        uid: {
            // 分享面板share_uid
            type: String, default: '', required: true,
        },
        apiPrefix: {
            // sdk内ajax请求 api 前缀，比如请求mysql 数据，/api/v1/datasource/query/,:api-prefix ='a',则请求地址为：a/api/v1/datasource/query/
            type: String, default: '',
        },
        timeRange: {
            // 面板筛选变量默认时间范围，默认值 ['now/d', 'now/d']
            type: Array, default: () => DEFAULT_TIME_RANGE,
        },
        filter: {
            // 面板筛选变量默认属性，{a:1,b:2}，会以此key、value覆盖 工具栏上筛选变量
            type: Object, default: () => ({}),
        },
        isFullScroll: {
            // 默认面板将100%充满容器，工具栏固定，此值为false，整个面板将会在容器内滚动
            type: Boolean, default: true,
        },
        isShowWaterMark: {
            // 面板图表是否覆盖水印
            type: Boolean, default: true,
        },
        isShowTools: {
            // 是否展示面板上的工具栏，值为false是，工具栏将不展示，工具栏的工具展示属性（如：）配置无效
            type: Boolean, default: true,
        },
        isShowRefresh: {
            // 是否展示定时刷新组件
            type: Boolean, default: true,
        },
        isShowTimeRange: {
            // 是否展示时间查询组件
            type: Boolean, default: true,
        },
    },
});
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


# 开发文档
[开发指南](README_DEV.md)

# 打包说明


