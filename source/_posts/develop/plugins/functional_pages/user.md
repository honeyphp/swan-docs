---
title: 用户信息功能页
header: develop
nav: plugins
sidebar: functional_pages_user
---
# 用户信息功能页

用户信息功能页用于帮助插件获取用户信息，包括 openid 和昵称等，相当于 [swan.login](/docs/develop/api/open/log_swan-login/) 和 [swan.getUserInfo](/docs/develop/api/open/userinfo_swan-getUserInfo/) 的功能。

用户在这个功能页中授权之后，插件就可以直接调用 swan.login 和 swan.getUserInfo 。无需再次进入功能页获取用户信息。

## 调用参数
用户信息功能页使用 functional-page-navigator 进行跳转时，对应的参数 name 应为固定值 loginAndGetUserInfo

bind:success 方法的返回参数说明：

|参数  |类型|说明 |
|---- | ---- |---- |
|userInfo  | Object  |用户信息对象, 参数说明按参考 [swan.getUserInfo](/docs/develop/api/open/userinfo_swan-getUserInfo/)|
|data  | String  |包括敏感数据在内的完整用户信息的加密数据，加解密逻辑参考[用户数据的签名验证和加解密](https://smartprogram.baidu.com/docs/develop/api/open_log/#%E7%94%A8%E6%88%B7%E6%95%B0%E6%8D%AE%E7%9A%84%E7%AD%BE%E5%90%8D%E9%AA%8C%E8%AF%81%E5%92%8C%E5%8A%A0%E8%A7%A3%E5%AF%86)。|
|iv | String | 加密算法的初始向量|

代码示例：

```
<!--plugin/components/hello-component.swan-->
  <functional-page-navigator
    name="loginAndGetUserInfo"
    version="develop"
    bind:success="loginSuccess"
    bind:fail="loginFail"
  >
    <button class="login">登录到插件</button>
  </functional-page-navigator>
// plugin/components/hello-component.js
Component({
  properties: {},
  data: {
  },
  methods: {
    loginSuccess: function (res) {
      console.log(res);
    },
    loginFail: function (res) {
      console.log(res);
    }
  }
});
```

