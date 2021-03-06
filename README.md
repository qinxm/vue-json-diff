# vue-json-diff

基于Fehelper里的jsondiff功能封装的vue组件。

推荐浏览器插件：FeHelper--Web前端助手(https://github.com/zxlie/FeHelper)

实在太香，忍不住安利！

## Links
- Github(https://github.com/qinxm/vue-json-diff)

## Usage

安装vue-json-diff包，依赖vue

```
npm install vue-json-diff
or
yarn add vue-json-diff
```

vue调用
```
<template>
  <div id="app">
    <json-diff :jsonSourceLeft="leftData" :jsonSourceRight="rightData" />
  </div>
</template>

<script>
import JsonDiff from 'vue-json-diff'
export default {
  components: {
    JsonDiff
  },
  data() {
    return {
      leftData: {
        "data": {
            "needQueryPosition": 0,
            "orderStatus": "已取消",
            "orderTrace": {
                "timeLine": [
                    {
                        "date": "10/13",
                        "time": "18:26",
                        "status": "订单已取消"
                    },
                    {
                        "date": "10/13",
                        "time": "18:11",
                        "status": "订单提交成功"
                    }
                ],
                "lastStatusDesc": "订单未支付，已自动取消"
            }
          
        },
        "code": 0,
        "msg": "",
        "success": true
      },
      rightData: {
          "data": {
              "needQueryPosition1": 0,
              "orderStatus": "已取消",
              "orderTrace1": {
                  "timeLine": [
                      {
                          "date": "10/13",
                          "time": "18:26",
                          "status": "订单已取消"
                      },
                      {
                          "date": "10/13",
                          "time": "18:11",
                          "status": "订单提交成功"
                      }
                  ],
                  "lastStatusDesc": "订单未支付，已自动取消"
              }
            
          },
          "code": 1,
          "msg": "2222",
          "success": true
      }
    }
  }
}
</script>
```

## props


属性 | 类型 | 描述
---|---|---
jsonSourceLeft | Object/String | 左侧区域展示数据
jsonSourceRight | Object/String | 右侧区域展示数据
showHeading | Boolean | 是否显示顶部对比结果
errorHandler | Function | 错误处理回调方法
diffHandler | Function | 对比结果回调方法

## PS ❤️
如果喜欢请给个星星，谢谢。 If you like, please give me a star, thank you.

如果需要帮助: QQ:1034688013 邮箱: 1034688013@qq.com if you need help: QQ:1034688013 email: 1034688013@qq.com


