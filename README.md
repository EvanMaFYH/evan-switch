# evan-switch
uniapp开关组件，支持双向数据绑定，支持切换前事件拦截   
测试过微信小程序、app（包括nvue模式）、h5

### 1.基本用法

```
﻿<evan-switch v-model="checked"></evan-switch>
```

### 2.更多用法
参考[github demo](https://github.com/EvanMaFYH/evan-switch)中的用法

### evan-switch props
| 参数           | 说明            | 类型    | 可选值     | 默认值  |    
| :-------------------- | :------------------------------ | :---------- | :-------- | :--- |  
| v-model | 开关选中状态 | string/number/boolean | - | false |
| active-color | 打开状态的颜色 | string | - | ﻿#108ee9 |
| inactive-color | 关闭状态的颜色 | string | - | #fff |
| disabled | 是否禁用 | boolean | - | false |
| size | 大小（单位px） | number | - | 30 |
| active-value | 打开时的value值 | string/number/boolean | - | true |
| inactive-value | 关闭时的value值 | string/number/boolean | - | false |
| before-change | 开关状态切换前的钩子，如果返回false或者返回Promise且被reject，则状态不会被切换，第一个参数为将要切换的状态，第二个参数为传递给组件的extraData | Function(nextStatus, extraData) | - | - |
| extra-data | 需要传递给组件的额外属性，通常配合before-change使用，在循环switch组件拦截的时候判断是哪一个swtich触发的 | any | - | - |

### evan-switch events
| name | 说明 | 回调参数 |
| :--- | :---------------- | ------------------|
| change | 开关状态变更 | 第一个是变更后的状态，第二个是传递的extraData参数 |
