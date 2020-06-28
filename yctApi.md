## 羊城通接口文档

### 接口访问域名：
#####   https://pubser-test.zhenai.com --测试
#####   https://pubser.zhenai.com --生产
         
#### MD5签名示例
```java
        /**
         * 先将参数排序
         */
        String[] strArray = { TOKEN, timestamp, nonce };
        Arrays.sort(strArray);
        StringBuilder sb = new StringBuilder();
        for (String str : strArray) {
            sb.append(str);
        }

    /**
	 * 然后用SHA1算法生成安全签名
	 *
	 * @param string1
	 * @return
	 */
	public static String getSignature(String string1) {
		StringBuffer hexstr = new StringBuffer(256);
		try {
			byte[] digest = MessageDigest.getInstance("SHA-1").digest(string1.getBytes());
			String shaHex = "";
			for (int i = 0; i < digest.length; i++) {
				shaHex = Integer.toHexString(digest[i] & 0xFF);
				if (shaHex.length() < 2) {
					hexstr.append(0);
				}
				hexstr.append(shaHex);
			}
		}catch (Exception e){
			throw new RedeeException("生成签名失败");
		}
		return hexstr.toString();
	}
```

## 错误码
| code | message |   说明   |
| :--------:   | :-----:  |  :-----:  |
| 200    | 成功  |  执行成功  |
| 600    | 必传参数不能为空  |  必填的参数未传  |
| 601    | 参数错误  |  传递错误的参数  |
| 602    | 数据不存在  |  该数据不存在  |
| 603    | 签名错误  |  签名校验错误  |

## **生成羊城通兑换码**

* POST `/datingapi/external/api/yct/generateCode`

**请求参数**
##Headers
| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| Content-Type    | application/json  |  yes  |    |

##Body
| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| signature    | String  |  是  |  签名  |
| timestamp   | String  |  是  |  时间戳（秒，和当前时间误差1分钟以内）  |
| nonce    | String  |  是  |  随机字符串  |
| orderId    | String  |  是  |  订单ID  |
| userId    | String  |  否  |  用户唯一主键  |
| phone    | String  |  否  |  手机号  |
| amount    | String  |  否  |  订单金额（分）  |

**返回值**

```json
{
  "code": 200,// 200成功，否则失败
  "msg": "成功",// 返回的信息
  "data": {//返回的数据
    "exchangeCode": "wp1mrkhjd8fXxNOy",//创建的兑换码
  }
}
```

**示例**
* `curl -X POST "https://pubser-test.zhenai.com/datingapi/external/api/yct/generateCode" -H "accept: */*" -H "Content-Type: application/json" -d "{\"signature\":\"5454541343dffdf\",\"timestamp\":\"1593329206\",\"nonce\":\"fdsfs\",\"orderId\":\"FGh55664433322\",\"userId\":\"89994856\",\"phone\":\"18664987481\",\"amount\":3990}"`
----
## **更新羊城通支付订单状态**

* POST `/datingapi/external/api/yct/syncCodeStatus`

**请求参数**
##Headers
| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| Content-Type    | application/json  |  yes  |    |

##Body
| 参数 | 类型 |  是否必须   |  说明   |
| :--------:   | :-----:  |  :-----:  |  :-----:  |
| signature    | String  |  是  |  签名  |
| timestamp   | String  |  是  |  时间戳（秒，和当前时间误差1分钟以内）  |
| nonce    | String  |  是  |  随机字符串  |
| orderId    | String  |  是  |  订单ID  |

**返回值**

```json
{
  "code": 200,// 200成功，否则失败
  "msg": "成功",// 返回的信息
  "data": {//返回的数据
    "orderId": "wp1mrkhjd8fXxNOy",//创建的兑换码
  }
}
```

**示例**
* `curl -X POST "https://pubser-test.zhenai.com/datingapi/external/api/yct/syncCodeStatus" -H "accept: */*" -H "Content-Type: application/json" -d "{\"signature\":\"5454541343dffdf\",\"timestamp\":\"1593329206\",\"nonce\":\"fdsfs\",\"orderId\":\"FGh55664433322\"}"`
----
