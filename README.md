# apidoc
接口文档

# 接口访问域名：https://api.mypays.net
### MD5签名示例：org.springframework.util.DigestUtils.md5DigestAsHex((apiSecret+time).getBytes())
## **创建商户api**

* POST `/api/apiKey/create`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| apiCode    | String  |  yes  |  商户自定义的apiCode  |
| apiName   | String  |  yes  |  商户名称  |
| callUrl    | String  |  yes  |  商户订单回调地址  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": {--返回的数据
    "createTime": "2019-08-12 03:32:44",--创建时间
    "updateTime": null,-- 修改时间
    "apiKeyId": 8,--唯一主键
    "apiId": "K1724260436",-- appid（后台生成）
    "apiSecret": "vcHJvE8XpvMAJsfR7tlp0A35NKXnb4Wk",--秘钥
    "apiCode": "dsadsad",
    "apiName": "sadsadas",
    "callUrl": "fsagagas"
  }
}
```

## **更新商户回调地址**

* PUT `/api/apiKey/update`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| apiCode    | String  |  yes  |  商户apiCode  |
| callUrl    | String  |  yes  |  商户订单回调地址  |
| sign     | String  |  yes  |  MD5(秘钥+时间戳)  |
| time     | long  |  yes  |  时间戳  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": {--返回的数据
    "createTime": "2019-08-12 03:32:44",--创建时间
    "updateTime": null,-- 修改时间
    "apiKeyId": 8,--唯一主键
    "apiId": "K1724260436",-- appid（后台生成）
    "apiSecret": "vcHJvE8XpvMAJsfR7tlp0A35NKXnb4Wk",--秘钥
    "apiCode": "dsadsad",
    "apiName": "sadsadas",
    "callUrl": "fsagagas"
  }
}
```

**示例**
* `curl -X PUT "http://localhost:5080/api/apiKey/update?apiCode=dsadsad&callUrl=ccccccc&sign=05e564d5dcc5ff5f8b6f5dfbc9a141eb&time=4466" -H "accept: */*"`
----

## **添加商户的支付方式**

* POST `/api/payway/addPayWay`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| account     | String  |  no  |  账号信息  |
| apiId    | String  |  yes  |  商户apiId  |
| remark    | String  |  no  |  备注  |
| sign     | String  |  yes  |  MD5(秘钥+时间戳)  |
| time     | long  |  yes  |  时间戳  |
| typeCode     | String  |  yes  |  类型【wechat-微信，alipay-支付宝,bankcard-银行卡，other-其他】  |
| typeName     | String  |  no  |  类型名称  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": {--返回的数据
    "createTime": "2019-08-12 03:51:55",--创建时间
    "updateTime": null,
    "payWayId": 6,--唯一主键
    "typeCode": "wechat",
    "typeName": "微信",
    "account": "2343343435",
    "remark": "测试",
    "apiId": "K1724260436"
  }
}
```

**示例**
* `curl -X POST "http://localhost:5080/api/payway/addPayWay?account=2343343435&apiId=K1724260436&remark=%E6%B5%8B%E8%AF%95&sign=05e564d5dcc5ff5f8b6f5dfbc9a141eb&time=4466&typeCode=wechat&typeName=%E5%BE%AE%E4%BF%A1" -H "accept: */*"`
----

## **删除商户的支付方式**

* POST `/api/payway/deletePayWay`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| payWayId      | String  |  yes  |  支付方式主键  |
| sign     | String  |  yes  |  MD5(秘钥+时间戳)  |
| time     | long  |  yes  |  时间戳  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": 6--返回的数据
}
```

**示例**
* `curl -X POST "http://localhost:5080/api/payway/deletePayWay?payWayId=6&sign=05e564d5dcc5ff5f8b6f5dfbc9a141eb&time=4466" -H "accept: */*"`
----


## **商户的支付方式列表**

* GET `/api/payway/payWayList`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| apiId    | String  |  yes  |  商户apiId  |
| sign     | String  |  yes  |  MD5(秘钥+时间戳)  |
| time     | long  |  yes  |  时间戳  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": [{--返回的数据
    "createTime": "2019-08-12 03:51:55",--创建时间
    "updateTime": null,
    "payWayId": 6,--唯一主键
    "typeCode": "wechat",
    "typeName": "微信",
    "account": "2343343435",
    "remark": "测试",
    "apiId": "K1724260436"
  }]
}
```

**示例**
* `curl -X GET "http://localhost:5080/api/payway/payWayList?apiId=K1724260436&sign=05e564d5dcc5ff5f8b6f5dfbc9a141eb&time=4466" -H "accept: */*"`
----

## **更新商户的支付方式**

* PUT `/api/payway/addPayWay`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| account     | String  |  no  |  账号信息  |
| payWayId      | Long  |  yes  |  支付方式主键  |
| remark    | String  |  no  |  修改后的备注  |
| sign     | String  |  yes  |  MD5(秘钥+时间戳)  |
| time     | Long  |  yes  |  时间戳  |
| typeCode     | String  |  yes  |   修改后的类型【wechat-微信，alipay-支付宝,bankcard-银行卡，other-其他】  |
| typeName     | String  |  no  |   修改后的类型名称  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败
  "msg": "成功",-- 返回的信息
  "data": {--返回的数据
    "createTime": "2019-08-12 03:51:55",--创建时间
    "updateTime": null,
    "payWayId": 6,--唯一主键
    "typeCode": "wechat",
    "typeName": "微信",
    "account": "2343343435",
    "remark": "测试",
    "apiId": "K1724260436"
  }
}
```

**示例**
* `curl -X PUT "http://localhost:5080/api/payway/updatePayWay?account=xxxxx&payWayId=6&remark=ffffffff&sign=05e564d5dcc5ff5f8b6f5dfbc9a141eb&time=4466&typeCode=alipay&typeName=dssds" -H "accept: */*"`
----

## **订单推送接口**

* POST `该接口由调用方提供，并在创建商户时配置`

**请求参数**

| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| orderId     | String  |  yes  |  订单主键  |
| orderNo      | String  |  yes  |  订单编号  |
| transTime    | Date  |  yes  |  交易时间（yyyy-MM-dd HH:mm:ss）  |
| amount     | BigDecimal  |  yes  |  支付金额  |
| title     | String  |  yes  |  标题  |
| contant     | String  |  yes  |  内容  |
| typeCode     | String  |  yes  |   支付类型【wechat-微信，alipay-支付宝,bankcard-银行卡，other-其他】  |
| typeName     | String  |  yes  |   支付中文名称  |
| apiId     | String  |  yes  |   商户apiId  |

**返回值**

```json
{
  "code": 0,-- 0成功，否则失败(失败会重复调用5次，5次后需要手工再触发调用或者每天会定时调用)
}
```
----
