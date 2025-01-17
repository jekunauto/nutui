#  countdown组件

### 介绍

### 安装


``` javascript
import { createApp } from 'vue';
// vue
import { CountDown } from '@nutui/nutui';
// taro
import { CountDown } from '@nutui/nutui-taro';

const app = createApp();
app.use(CountDown);
```

### 基础用法

```html
<nut-countdown :end-time="end" ></nut-countdown>
```

``` javascript
setup() {
  const state = reactive({
      end: Date.now() + 50 * 1000,
    });
  return {
    ...toRefs(state)
  };
}
```

### 显示天

```html
<nut-countdown :end-time="end" show-days ></nut-countdown>
```

### 以服务端的时间为准

```html
<nut-countdown  :start-time="serverTime" :end-time="end" show-days ></nut-countdown>
```

``` javascript
setup() {
  const state = reactive({
      serverTime: Date.now() - 30 * 1000,
      end: Date.now() + 50 * 1000,
    });
  return {
    ...toRefs(state)
  };
}
```

### 显示为 天时分秒

```html
<nut-countdown show-days show-plain-text  :end-time="end"></nut-countdown>
```
``` javascript
setup() {
  const state = reactive({
      end: Date.now() + 50 * 1000,
    });
  return {
    ...toRefs(state)
  };
}
```

### 异步更新结束时间

```html
<nut-countdown  show-days show-plain-text  :end-time="asyncEnd" ></nut-countdown>
```
``` javascript
setup() {
  const state = reactive({
      asyncEnd: 0,
    });
  return {
    ...toRefs(state)
  };
}
```

### 控制开始和暂停的倒计时

```html
<nut-cell>
    <nut-countdown  :endTime="end" :paused="paused" @on-paused="onpaused" @on-restart="onrestart" />
    <div style="position:absolute;right:10px;top:9px">
        <nut-button type="primary" size='small' @click="toggle">{{ paused ? 'start' : 'stop' }}</nut-button>
    </div>
</nut-cell>
```
``` javascript
setup() {
  const state = reactive({
      paused: false,
      end: Date.now() + 50 * 1000,
    });

    const toggle = ()=> {
      state.paused = !state.paused;
    }
    const onpaused = (v)=> {
      console.log('paused: ', v);
    }
    const onrestart = (v)=> {
      console.log('restart: ', v);
    }
  return {
      toggle,
      onpaused,
      onrestart,
    ...toRefs(state)
  };
}
```
### 自定义展示

```html
<nut-countdown v-model="resetTime" :endTime="end">
    <div class="countdown-part-box">
        <div class="part-item-symbol"> resetTime.d 天</div>
        <div class="part-item h"> resetTime.h </div>
        <span class="part-item-symbol">:</span>
        <div class="part-item m"> resetTime.m </div>
        <span class="part-item-symbol">:</span>
        <div class="part-item s"> resetTime.s </div>
    </div>
</nut-countdown>
```
``` javascript
setup() {
  const state = reactive({
      end: Date.now() + 50 * 1000,
      resetTime: {
        d: '1',
        h: '00',
        m: '00',
        s: '00'
      }
    });
  return {
    ...toRefs(state)
  };
}
```

### API

### Props

| 字段 | 说明 | 类型 | 默认值
| ----- | ----- | ----- | -----
| v-model | 当前时间，自定义展示内容时生效 | Object | {}
| start-time | 开始时间 | String, Number | Date.now()
| end-time | 结束时间 | String, Number | Date.now()
| show-days | 是否显示天 | Boolean | false
| show-plain-text | 显示为纯文本 | Boolean | false
| paused | 是否暂停 | Boolean | false


### Event

| 字段 | 说明 | 回调参数
| ----- | ----- | ----- 
| on-end | 倒计时结束时 | 剩余时间戳
| on-paused | 暂停时 | 剩余时间戳
| on-restart | 暂停时 | 剩余时间戳