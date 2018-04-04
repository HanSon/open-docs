## 第三方订单接收

### 请求地址

正式环境：https://erp.cblink.net/openapi/trade

### 请求方式

POST
Content-type: application/json

### 请求头

|字段|类型|是否必须|示例|描述|
|---|---|---|---|---|
|App-Id|string|是|cb17333123|cblink 的 appid|
|App-Secret|string|是|63d2ccdcdc8916daxasdadsab043f0948|cblink 的 appid 对应的 secret|
|Content-Type|string|是|application/json|传输 json 数据|
|Accept|string|是|application/json|如有错误，将会以 json 返回|

### 请求参数

trade

|字段|类型|是否必须|描述|
|---|---|---|---|
|tid|String|是|交易编号|
|shop_id|Integer|是|门店ID|
|serial_number|String|是|当天流水号|
|transaction_tid|String|是|支付流水号|
|type|String|是|交易类型 "COD", "FIXED", "GROUP", "PEER", "QRCODE", "WAIMAI"|
|title|Integer|是|首个商品标题|
|total_fee|Integer|是|该笔交易应付金额|
|payment|Integer|是|该笔交易实付金额|
|post_fee|Integer|是|运费|
|discount_fee|Integer|是|优惠金额 0|
|adjust_fee|Integer|是|改价金额 0|
|remark|String|是|客户留言|
|pay_type|Integer|是|支付类型 "", "ALIPAY", "BAIDUPAY", "BANKCARDPAY", "CODPAY", "COUPONPAY", "ECARD", "COUPONPAY", "ONLINE", "PEERPAY", "WEIXIN", "WEIXIN_DAIXIAO"|
|handled|Integer|是|结算状态 1|
|status|Integer|是|状态 "TRADE_BUYER_REFUND", "TRADE_BUYER_SIGNED", "TRADE_CLOSED", "TRADE_CLOSED_BY_USER", "TRADE_INVALID", "TRADE_REFUNDING", "WAIT_BUYER_CONFIRM_GOODS", "WAIT_BUYER_PAY", "WAIT_SELLER_SEND_GOODS", "WAIT_USE"|
|shipping_type|Integer|是|创建交易时的物流方式 "express", "fetch", "local", "no_shipping"|
|created_at|String|是|创建时间|
|updated_at|String|是|更新时间|
|pay_at|String|否|支付时间|
|refund_status|String|否|退款状态 "", "CLOSED", "REFUNDING", "SELLER_REFUSE_BUYER", "TRADE_CLOSED", "TRADE_REFUNDING", "WAIT_SELLER_AGREE"|
|member|Object|是|查看下方 Member|
|Orders|Array|是|查看下方 Order|

member

|字段|类型|是否必须|描述|
|---|---|---|---|
|weixin_open_id|String|是|微信openid|
|name|String|是|收货人|
|mobile_phone|String|是|收货人联系电话|
|gender|String|是|收货人性别|
|gender|String|是|收货人性别|
|receiver_province|String|是|收货人省|
|receiver_city|String|是|收货人城市|
|receiver_district|String|是|收货人区|
|receiver_zip|String|否|收件人邮编|
|lat|String|否|收件人经度|
|lng|String|否|收件人纬度|

order

|字段|类型|是否必须|描述|
|---|---|---|---|
|product_id|String|是|商品id|
|num|String|是|数量|
|product_specification|String|是|规格|
|title|String|是|商品名称|
|pic_thumb_url|String|是|商品主图片缩略图地址|
|price|String|是|商品单价|
|total_fee|String|是|同样商品 x 份数 得到的总价|
|payment|String|是|该商品实际支付价格|
|discount_fee|String|否|该商品优惠价格|
|cart_id|String|否|口袋|


请求示例
```
{
  "tid": "5cC4A4Bc-c4aA-8ecB-5C52-c48e7E1882cC",
  "shop_id": 20,
  "serial_number": 1,
  "transaction_tid": "bbf7896E-dDc3-DA4B-e985-7dDe1D6d3D7c",
  "type": "COD",
  "title": "半什持并去任学",
  "total_fee": 75.08,
  "payment": 26.01,
  "post_fee": 5,
  "discount_fee": 9.73,
  "adjust_fee": 8,
  "remark": "留言信息",
  "pay_type": "OFFLINE",
  "handled": 1,
  "status": "TRADE_BUYER_SIGNED",
  "shipping_type": "express",
  "refund_status": null,
  "pay_at": null,
  "created_at": "2018-04-02 14:44:46",
  "updated_at": "2018-04-02 14:44:46",
  "member": {
    "weixin_openid": "weixin_openid",
    "name": "张三",
    "mobile_phone": 13333333333,
    "gender": 1,
    "receiver_province": "福建",
    "receiver_city": "昌平区",
    "receiver_district": "回龙观",
    "receiver_address": "南安市水头镇福兴街"
  },
  "orders": [
    {
      "product_id": 11,
      "status": "FINISH",
      "num": 12,
      "product_specification": "大",
      "title": "堕落虾",
      "pic_thumb_url": "http://baidu.com",
      "price": 200,
      "total_fee": 400,
      "payment": 300
    }
  ]
}
```

### 成功响应参数

|字段|类型|是否必须|示例|描述|
|---|---|---|---|
|code|int|是||返回响应码|
|data|string|是||数据|

### 成功响应示例

```
{
    "code": 200,
    "data": ""
}
```

### 失败响应参数

|字段|类型|是否必须|示例|描述|
|---|---|---|---|
|err_code|int|是||返回错误码|
|msg|string|是||返回错误信息|

### 失败响应示例

```
{
    "err_code": 400,
    "msg": "tid 不能为空。"
}
```