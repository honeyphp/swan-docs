---
title: 支付功能页
header: develop
nav: plugins
sidebar: functional_pages_payment
---
# 支付功能页
支付功能页用于帮助插件完成支付，相当于 [swan.requestPolymerPayment](/docs/develop/api/open/payment_swan-requestPolymerPayment/) 的功能。

## 调用参数
支付功能页使用 functional-page-navigator 进行跳转时，对应的参数 name 应为固定值 requestPayment，其他参数如下：

args参数说明：

|参数名|类型|必填|说明|
|----|----|----|----|
|fee|Number|是|需要显示在页面中的金额，单位为分|
|paymentArgs|Object|否|任意数据，传递给功能页中的响应函数|
|currencyType|String|否|需要显示在页面中的货币符号的代码，默认为 CNY|

代码示例：

```
<!-- plugin/components/pay.swanml -->
<!-- 上线时，version 应改为 "release"，并确保插件所有者小程序已经发布 -->
<functional-page-navigator
  version="develop"
  name="requestPayment"
  args="{{ args }}"
  bind:success="paymentSuccess"
  bind:fail="paymentFailed"
>
  <button class="payment-button">支付 0.01 元</button>
</functional-page-navigator>
// plugin/components/pay.js
Component({
  data: {
    args: {
      fee: 1,             // 支付金额，单位为分
      paymentArgs: 'A', // 将传递到功能页函数的自定义参数
      currencyType: 'USD' // 货币符号，页面显示货币简写 US$ 
    }
  },
  methods: {
    // 支付成功的回调接口
    paymentSuccess: function (e) {
      console.log(e);
    },
    // 支付失败的回调接口
    paymentFailed: function (e) {
      console.log(e);
    }
  }
})
```

用户点击该 navigator 后，将跳转到支付功能页

## 配置功能页函数
支付功能页需要插件开发者在插件所有者小程序中提供一个函数来响应插件中的支付调用。即，在插件中跳转到支付功能页时，这个函数就会在合适的时机被调用，来帮助完成支付。如果不提供功能页函数，功能页调用将通过 fail 事件返回失败。

支付功能页函数应以导出函数的形式提供在插件所有者小程序的根目录下的 functional-pages/request-payment.js 文件中，名为 beforeRequestPayment。该函数应接收两个参数：

|参数名|类型|说明|
|----|----|----|
|paymentArgs|Object|即通过 functional-page-navigator 的 arg 参数中的 paymentArgs 字段传递到功能页的自定义数据|
|callback|Function|回调函数，调用该函数后，小程序将发起支付（类似于 swan.requestPolymerPayment）|


callback函数的参数：

|参数名|类型|说明|
|----|----|----|
|error|Object|失败信息，若无失败，应返回 null|
|requestPaymentArgs|Object|用于发起支付，和 swan.requestPolymerPayment 的参数相同，但没有回调函数（success, fail, complete），用于调用 swan.requestPolymerPayment，参考：[swan.requestPolymerPayment](/docs/develop/api/open/payment_swan-requestPolymerPayment/)|


## 功能页函数代码示例：

```
// functional-pages/request-payment.js

exports.beforeRequestPayment = function (paymentArgs, callback) {
    // 支付能力参数组装，在此之前，开发者自行进行登录、与开发者服务端交互的操作，完成支付参数组装。
    // callback 执行支付逻辑
    // paymentArgs 从插件中传递过来的开发者自定义参数
    console.log(paymentArgs);
    let payment = {
        "orderInfo":{
            "dealId":"xxx",
            "totalAmount":"1",
            "tpOrderId":"xxxxx",
            "dealTitle":"百度小程序Demo支付测试",
            "bizInfo":"...",
            "appKey":"MMMzUX",
            "rsaSign":"xxxxxx\/xxxxxx+\/T\/xxxxxx\/xxxx\/xxxx+xxxx=",
            "signFieldsRange":"1"
        },
        "from":"swan"
    };
    // error 在过程中进行捕获异常，如果callback接收到了error，则支付终端。
    let error = null;
    callback(error, payment);
}
```

注意：功能页函数不应 require 其他非 functional-pages 目录中的文件，其他非 functional-pages 目录中的文件也不应 require 这个目录中的文件。

这个目录和文件应当被放置在插件所有者小程序代码中（而非插件代码中），它是插件所有者小程序的一部分（而非插件的一部分）。 如果需要新增或更改这段代码，需要发布插件所有者小程序，才能在正式版中生效；需要重新预览插件所有者小程序，才能在开发版中生效。