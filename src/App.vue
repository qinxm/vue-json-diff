<template>
  <div id="app">
    <json-diff :jsonSourceLeft="leftData" :jsonSourceRight="rightData" />
  </div>
</template>

<script>
import JsonDiff from './components/jsonDiff/index.vue'
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
