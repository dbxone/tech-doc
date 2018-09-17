## 获取存储费率

获取数据存储的费率（以KB为单位）

## 请求地址

GET /api/storeFee

## 请求参数

## 响应参数

| 参数 | 类型 | 是否必填 | 最大长度 | 描述 | 示例 |
| --- | --- | --- | --- | --- | --- |
| price\_per\_kbyte | Number | Y |  | 每KB需要的DBX数，整数 | 20，实际为20/100000即0.00002DBX/KB |

```
price_per_kbyte: 确保整数,金额 = 100000 * 实际金额
```

例子

```js
{
    "code":200,
    "msg":"ok",
    "data":{
        "price_per_kbyte":20
    }
}
```

## SDK示例-JAVA

```java
GetStoreDataFeeReq request = new GetStoreDataFeeReq();
GxbClient dbxClient = new GxbDefaultClient(storeUrl);
// 获取返回
GetStoreDataFeeResp resp = dbxClient.execute(request);
```

## 错误情况



