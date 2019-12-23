---
title: 导航
header: develop
nav: component
sidebar: nav
---

## navigator

**解释**：  页面链接，控制小程序的跳转，既可在当前小程序内部进行跳转，也可跳转至其他小程序。

> `navigator` 的子节点背景色应为透明色。


|属性名 |类型  |默认值  | 必填 |说明|最低版本|
|---- | ---- | ---- |---- |---- |---- |
|target|	String|	self| 否 |在哪个目标上发生跳转，默认当前小程序，可选值self/miniProgram|2.5.2|
| url | String |   | 否 |应用内的跳转链接 |-|
|open-type | String  | navigate  | 否 |跳转方式|-|
|delta | Number |  | 否 |当 open-type 为 'navigateBack' 时有效，表示回退的层数|-|
|app-id|	String| | 否 |	当target="miniProgram"时有效，要打开的小程序 App Key (小程序后台设置-开发设置中)|	2.5.2
|path|	String| | 否 | 当target="miniProgram"时有效，打开的页面路径，如果为空则打开首页。|	2.5.2|
|extra-data|	Object| | 否 |	当target="miniProgram"时有效，需要传递给目标小程序的数据，目标小程序可在 App.onLaunch()，App.onShow() 中获取到这份数据。<a href="https://smartprogram.baidu.com/docs/develop/framework/app_service_register/">详情</a>|	2.5.2|
|version|	version|	release| 否 | 当target="miniProgram"时有效，要打开的小程序版本，有效值 develop（开发版），trial（体验版），release（正式版），仅在当前小程序为开发版或体验版时此参数有效；如果当前小程序是正式版，则打开的小程序必定是正式版。|2.5.2|
|hover-class | String  |navigator-hover | 否 |指定点击时的样式类，当`hover-class="none"`时，没有点击态效果。||
|hover-stop-propagation | Boolean  | false | 否 |指定是否阻止本节点的祖先节点出现点击态。|-|
|hover-start-time |Number | 50  | 否 | 按住后多久出现点击态，单位毫秒。 |-|
|hover-stay-time |Number |600 | 否 |手指松开后点击态保留时间，单位毫秒。|-|
|bindsuccess|	String| | 否 |		当target="miniProgram"时有效，跳转小程序成功。|	2.5.2|
|bindfail|	String| | 否 |当target="miniProgram"时有效，跳转小程序失败。|	2.5.2|
|bindcomplete|	String|  | 否 |		当target="miniProgram"时有效，跳转小程序完成。|	2.5.2|

**target 有效值**:

| 值 | 说明 |
| ---- | ---- |
| self | 当前小程序 |
| miniProgram | 跳转到另一个小程序 |

**version 有效值**:

| 值 | 说明 |
| ---- | ---- |
| develop | 开发版 |
| trial | 体验版 |
| release | 正式版 |

**open-type 有效值**：

|值 |说明 |最低版本|
|--- |--- |--- |
| navigate | 对应 <a href="https://smartprogram.baidu.com/docs/develop/api/show_tab/#swan-navigateTo/">`swan.navigateTo`</a> 的功能|-|
| redirect | 对应 <a href="https://smartprogram.baidu.com/docs/develop/api/show_tab/#swan-redirectTo/">`swan.redirectTo` </a> 的功能|-|
| switchTab | 对应 <a href="https://smartprogram.baidu.com/docs/develop/api/show_tab/#swan-switchTab/">`swan.switchTab ` </a> 的功能|-|
| navigateBack | 对应 <a href="https://smartprogram.baidu.com/docs/develop/api/show_tab/#swan-navigateBack/">`swan.navigateBack `</a>  的功能|-|
| reLaunch | 对应 <a href="https://smartprogram.baidu.com/docs/develop/api/show_tab/#swan-reLaunch/">`swan.reLaunch `</a>  的功能|-|
|exit|	退出小程序，target="miniProgram"时生效|	2.5.2|


**说明**:
`navigator-hover` 默认为:
```css
{
	background-color: rgba(0, 0, 0, 0.1);
	opacity: 0.7;
}
```

**示例**：
<a href="swanide://fragment/497f08f7f358abef70289b1c0b2193951560859565473" title="在开发者工具中预览效果" target="_blank">在开发者工具中预览效果</a>

* 在 swan 文件中

```html
<button type="primary" class="btn">
	<navigator class="nav" url="/pages/navigate/navigate" hover-class="navigator-hover">跳转到新页面</navigator>
</button>
<button type="primary" class="btn">
	<navigator class="nav" url="/pages/detail/detail" open-type="redirect" hover-class="other-navigator-hover">在当前页打开</navigator>
</button>
<button type="primary" class="btn">
	<navigator class="nav" url="/pages/index/index" open-type="switchTab" hover-class="other-navigator-hover">切换 Tab</navigator>
</button>
<button type="primary" class="btn">
  	<navigator class="nav" target="miniProgram" open-type="navigate" app-id="79RKhZ2BTvyyHitg4W3Xle4kkFgwwXyp" path="" extra-data="" version="release" bindsuccess="successHandler" bindfail="failHandler">打开绑定的小程序</navigator>
</button>
```


* 在 css 文件中

```css
.btn {
    margin: .15rem .23rem 0;
}
.nav {
    display: block;
}
```

* 在 js 文件中

```js
Page({
    data: {},
    successHandler: function (e) {
        console.log('success');
    },
    failHandler: function (e) {
        console.log('success');
    }
});
```

## functional-page-navigator

**解释**：仅在插件中有效，用于跳转到插件功能页。基础库 v3.120.0 开始支持，低版本需做[兼容处理](https://smartprogram.baidu.com/docs/develop/swan/compatibility/)。

###  属性说明 

| 属性名 | 类型  | 默认值  | 必填 | 说明 | 最低版本 |
| :---- | :---- | :---- |:---- | :---- | :---- |
| version | String | release | 否 | 跳转到的小程序版本，线上版本必须为正式版 | 3.120.0 |
| name | String |  | 否 | 要跳转到的功能页 | 3.120.0 |
| args | Object |  | 否 | 功能页参数，参数格式与具体功能页相关 | 3.120.0 |
| bindsuccess | EventHandle |  | 否 | 功能页返回，且操作成功时触发，detail格式与具体功能页相关 | 3.120.0 |
| bindfail | EventHandle |  | 否 | 功能页返回，且操作失败时触发，detail格式与具体功能页相关 | 3.120.0 |

#### version 有效值

| 值 | 说明 | 最低版本 |
|---|---|---|
| develop | 开发版 | 3.120.0 |
| trial | 体验版 | 3.120.0 |
| release | 正式版 | 3.120.0 |

#### name 有效值

| 值 | 说明 | 最低版本 |
|---|---|---|
| loginAndGetUserInfo | [用户信息功能页](/develop/plugins/functional_pages/user/) | 3.120.0 |
| requestPayment | [支付功能页](/develop/plugins/functional_pages/payment/) | 3.120.0 |
| chooseAddress | [收获地址功能页](/develop/plugins/functional_pages/address/) | 3.120.0 |


### Bug & Tip

* Tip: 功能页是插件所有者小程序中的一个特殊页面，开发者不能自定义这个页面的外观。

* Tip: 这个组件本身可以在开发者工具中使用，但功能页的跳转目前不支持在开发者工具中调试，请在真机上测试。


### 示例代码

```xml
<functional-page-navigator
    name="loginAndGetUserInfo"
    version="develop"
    bind:success="loginSuccess"
    bind:fail="loginFail">
    <button class="login">登录到插件</button>
</functional-page-navigator>
```

```js
Component({
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