# 支付中台接口说明

## 1. 微信支付相关接口

### 1.1 核心支付接口

**文件路径：** `pay-thirdplatform/src/main/java/com/csdn/mp/pay/thirdplatform/handler/wechat/WechatPayHandler.java`

| 接口方法 | 功能描述 | 调用方式 |
| --- | --- | --- |
| `createOrder()` | 统一下单 - 创建微信支付订单 | `POST https://api.mch.weixin.qq.com/pay/unifiedorder` |
| `queryOrder()` | 查询订单 - 查询微信支付订单状态 | `POST https://api.mch.weixin.qq.com/pay/orderquery` |
| `refundOrder()` | 申请退款 | `POST https://api.mch.weixin.qq.com/secapi/pay/refund`（需 SSL 证书） |
| `closeOrder()` | 关闭订单 | `POST https://api.mch.weixin.qq.com/pay/closeorder` |
| `cashWithdraw()` | 企业付款/提现 | `POST https://api.mch.weixin.qq.com/mmpaymkttransfers/promotion/transfers` |

### 1.2 微信签约相关接口

**文件路径：** `pay-thirdplatform/src/main/java/com/csdn/mp/pay/thirdplatform/handler/wechat/WechatPaySigning.java`

| 接口方法 | 功能描述 | 调用方式 |
| --- | --- | --- |
| `signingApp()` | APP 签约 | `POST https://api.mch.weixin.qq.com/papay/preentrustweb` |
| `signingH5()` | H5 签约 | `GET https://api.mch.weixin.qq.com/papay/h5entrustweb` |
| `signingPayment()` | 支付中签约 | `POST https://api.mch.weixin.qq.com/pay/contractorder` |
| `applyDeduction()` | 申请扣款 | `POST https://api.mch.weixin.qq.com/pay/pappayapply` |
| `applyRelieve()` | 申请解约 | `POST https://api.mch.weixin.qq.com/papay/deletecontract` |

### 1.3 回调接口

**文件路径：** `pay-service/src/main/java/com/csdn/mp/pay/controller/CallbackController.java`

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/thirdpay/callback/wx/pay` | 微信支付回调 | POST |
| `/thirdpay/callback/wx/refund` | 微信退款回调 | POST |
| `/thirdpay/callback/miniapp/pay` | 微信小程序支付回调 | POST |
| `/thirdpay/callback/wx/signing` | 微信签约/解约回调 | POST |

---

## 2. 支付宝相关接口

### 2.1 核心支付接口

**文件路径：** `pay-thirdplatform/src/main/java/com/csdn/mp/pay/thirdplatform/handler/alipay/AliPayHandler.java`

| 接口方法 | 功能描述 | 调用方式 |
| --- | --- | --- |
| `createOrder()` | 统一收单线下交易预创建 | 使用 Alipay SDK |
| `queryOrder()` | 统一收单线下交易查询 | 使用 Alipay SDK `AlipayTradeQueryRequest` |
| `refundOrder()` | 统一收单交易退款 | 使用 Alipay SDK `AlipayTradeRefundRequest` |
| `closeOrder()` | 统一收单交易关闭 | 使用 Alipay SDK `AlipayTradeCloseRequest` |
| `cashWithdraw()` | 单笔转账到支付宝账户 | 使用 Alipay SDK `AlipayFundTransUniTransferRequest` |
| `balanceQuery()` | 查询支付宝账户余额 | 使用 Alipay SDK `AlipayDataBillBalanceQueryRequest` |

### 2.2 回调接口

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/thirdpay/callback/alipay/pay` | 支付宝支付回调 | POST |
| `/thirdpay/callback/alipay/refund` | 支付宝退款回调 | POST |
| `/thirdpay/callback/alipay/signing` | 支付宝签约/解约回调 | POST |

---

## 3. iOS 相关接口

### 3.1 核心支付接口

**文件路径：** `pay-thirdplatform/src/main/java/com/csdn/mp/pay/thirdplatform/handler/iospay/IOSPayHandle.java`

| 接口方法 | 功能描述 | 调用方式 |
| --- | --- | --- |
| `createOrder()` | 创建 iOS 内购支付订单 | 发送 RocketMQ 消息异步处理 |
| `refundOrder()` | iOS 退款 | 内部处理 |

### 3.2 iOS 支付查询接口

**文件路径：** `pay-service/src/main/java/com/csdn/mp/pay/controller/IOSPayController.java`

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/ios/pay/getIosPayTransactionInfo` | 获取 iOS 交易信息 | GET |
| `/ios/pay/getTransactionInfoByIosOrderId` | 根据 iOS 订单号获取交易信息 | GET |
| `/ios/pay/getIosHistoryInfo` | 获取 iOS 交易历史 | GET |
| `/ios/pay/getIosSubscriptionInfo` | 获取 iOS 订阅信息 | GET |
| `/ios/pay/getIosRefundInfo` | 获取 iOS 退款信息 | GET |

### 3.3 iOS 签约续费订单接口

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/order/pay/iosContractPay` | 创建 iOS 签约续费支付订单 | POST |

---

## 4. 鸿蒙（HarmonyOS）相关接口

### 4.1 核心支付接口

**文件路径：** `pay-thirdplatform/src/main/java/com/csdn/mp/pay/thirdplatform/handler/harmonypay/HarmonyPayHandle.java`

| 接口方法 | 功能描述 | 调用方式 |
| --- | --- | --- |
| `createOrder()` | 创建鸿蒙内购支付订单 | 发送 RocketMQ 消息异步处理 |
| `refundOrder()` | 鸿蒙退款 | 内部处理 |

### 4.2 鸿蒙签约续费订单接口

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/order/pay/harmonyContractPay` | 创建鸿蒙签约续费支付订单 | POST |

---

## 5. 通用订单接口

**文件路径：** `pay-service/src/main/java/com/csdn/mp/pay/controller/OrderController.java`

| 接口路径 | 功能描述 | 请求方式 |
| --- | --- | --- |
| `/order/pay/create` | 创建支付订单 | POST |
| `/order/pay/close` | 关闭支付订单 | POST |
| `/order/recharge/create` | 创建充值订单 | POST |
| `/order/refund/create` | 创建退款订单 | POST |
| `/order/transfer/create` | 创建转账订单 | POST |
| `/order/cashWithdraw/create` | 创建提现订单 | POST |
| `/order/settlement/create` | 创建分账订单 | POST |

---

## 总结

这是一个完整的支付中台系统，主要特性如下：

1. **微信支付：** 支持统一下单、查询、退款、关闭订单、企业付款，以及完整的签约/扣款/解约体系。
2. **支付宝：** 使用支付宝 SDK 实现统一下单、查询、退款、关闭、转账、余额查询等功能。
3. **iOS 内购：** 通过 RocketMQ 异步处理，支持 StoreKit 1 和 StoreKit 2。
4. **鸿蒙内购：** 类似 iOS，通过 RocketMQ 异步处理，支持订阅续费。
