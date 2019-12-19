---
title: 收货地址功能页
header: develop
nav: plugins
sidebar: functional_pages_address
---
# 收货地址功能页

用户信息功能页使用 functional-page-navigator 进行跳转。
对应的参数 name 应为固定值 chooseAddress 。
bind:success 方法的返回参数与 [swan.chooseAddress](docs/develop/api/open/chooseaddress_swan-chooseAddress/) 相同。

## 代码示例：

```
<!--plugin/components/hello-component.swanml-->
  <functional-page-navigator
    name="chooseAddress"
    version="develop"
    bind:success="onSuccess"
    bind:fail="onFail"
  >
    <button>选择收货地址</button>
  </functional-page-navigator>
// plugin/components/hello-component.js
Component({
  methods: {
    onSuccess: function (res) {
      console.log(res.detail);
    },
    onFail: function (res) {
      console.log(res);
    }
  }
});
```