<template>
  <div class="wrapper wp-json" id="pageContainer">
     <div class="panel panel-default" style="margin-bottom: 0px;">
        <div class="panel-heading" v-if="showHeading">
            <h3 class="panel-title">
                <span class="x-error" v-bind:class="{'x-hlt' : errorHighlight}" v-html="errorMessage"></span>
            </h3>
        </div>
    </div>
    <div class="panel-body mod-json">
      <div class="col-md-6 box-wrapper-left">
        <textarea
          class="form-control mod-textarea jsonSourceLeft"
          id=""
          ref="srcLeft"
          placeholder="在这里粘贴JSON代码"
        >{{ leftData }}</textarea>
      </div>
      <div class="col-md-6 box-wrapper-right">
        <textarea
          class="form-control mod-textarea jsonSourceRight"
          ref="srcRight"
          placeholder="在这里粘贴JSON代码"
        >{{ rightData }}</textarea>
      </div>
    </div>
  </div>
</template>

<script>
import {JsonDiff}  from './static/index.js'

export default {
  name: "JsonDiff",
  props: {
    jsonSourceLeft: String | Object,
    jsonSourceRight: String | Object,
    showHeading: {
      type: Boolean,
      default: true
    },
    errorHandler: Function,
    diffHandler: Function

  },
  watch: {
    jsonSourceLeft: {
      handler(nVal, oVal) {
        //使用四个空格缩进
        this.leftData = JSON.stringify(nVal, null, 4);
      },
      deep: true,
      immediate: true
    },
    jsonSourceRight: {
      handler(nVal, oVal) 
      {
        //使用四个空格缩进
        this.rightData = JSON.stringify(nVal, null, 4);
      },
      deep: true,
      immediate: true
    }
  },
  data() {
    return {
      errorMessage: "",
      errorHighlight: false,
      leftData: "",
      rightData: ""
    };
  },
  mounted: function() {
    // 错误处理器
    let errorHandler = (which, ok) => {
      // debugger
      if (ok) {
        this.errorMessage = "两侧JSON比对完成！";
        this.errorHighlight = false;
      } else {
        this.errorMessage =
          { left: "左", right: "右", "left-right": "两" }[which] +
          "侧JSON不合法！";
        this.errorHighlight = true;
      }
    };

    // diff处理器
    let diffHandler = diffs => {
        console.log(diffs)
      if (!this.errorHighlight) {
        if (diffs.length) {
          this.errorMessage += "共有 " + diffs.length + " 处不一致！";
        } else {
          this.errorMessage += "左右两侧JSON内容一致！";
        }
      }
    };
    
    
    // 代码比对
    JsonDiff.init(
      this.$refs.srcLeft,
      this.$refs.srcRight,
      errorHandler,
      diffHandler
    );
    JsonDiff.compareJson()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url("./static/css/codemirror.css");
/* @import url("./bootstrap.min.css"); */

.clearfix:before, .clearfix:after, .dl-horizontal dd:before, .dl-horizontal dd:after, .container:before, .container:after, .container-fluid:before, .container-fluid:after, .row:before, .row:after, .form-horizontal .form-group:before, .form-horizontal .form-group:after, .btn-toolbar:before, .btn-toolbar:after, .btn-group-vertical>.btn-group:before, .btn-group-vertical>.btn-group:after, .nav:before, .nav:after, .navbar:before, .navbar:after, .navbar-header:before, .navbar-header:after, .navbar-collapse:before, .navbar-collapse:after, .pager:before, .pager:after, .panel-body:before, .panel-body:after, .modal-footer:before, .modal-footer:after {
    display: table;
    content: " ";
}
.clearfix:after, .dl-horizontal dd:after, .container:after, .container-fluid:after, .row:after, .form-horizontal .form-group:after, .btn-toolbar:after, .btn-group-vertical>.btn-group:after, .nav:after, .navbar:after, .navbar-header:after, .navbar-collapse:after, .pager:after, .panel-body:after, .modal-footer:after {
    clear: both;
}
.col-md-6 {
    width: 50%;
    float: left;
    position: relative;
    min-height: 1px;
}
.wp-json {
  width: auto;
}
.wp-json .CodeMirror {
  height: auto;
}
.wp-json .mod-json {
  position: absolute;
  top: 60px;
  bottom: 0;
  right: 20px;
  left: 20px;
}
.wp-json .mod-json .panel-txt {
  position: absolute;
  width: 500px;
  top: 15px;
  bottom: 0;
}
.wp-json .panel-body {
  padding: 15px 0;
  display: flex;
}
.wp-json .CodeMirror-scroll {
  min-height: 550px;
}

.box-wrapper-left {
  height: 100%;
  padding: 0 5px 0 0;
}
.box-wrapper-right {
  height: 100%;
  padding: 0 0 0 5px;
}
.jsonSourceLeft,
.jsonSourceRight,
.CodeMirror {
  height: calc(100%);
  font-size: 10px;
}
.x-error {
  float: right;
  color: #0c0;
  font-size: 14px;
}
.x-error.x-hlt {
  color: #f00;
}
</style>
