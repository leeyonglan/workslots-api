# 线下充值/下分接口文档

## 1. 线下支付操作

### 1.1 线下充值/下分操作

**接口地址:** `/admin/offlinepay/offlineopt`

**请求方法:** POST

**请求参数:**

| 字段名    | 类型     | 必填 | 说明                     |
| ------ | ------ | -- | ---------------------- |
| type   | int    | 是  | 操作类型：1-上分(充值)，2-下分(兑换) |
| uid    | int64  | 是  | 用户ID                   |
| amount | int64  | 是  | 金额，单位为金币               |
| mark   | string | 否  | 操作备注                   |

**上分(充值)备注：** 会显示在充值查询的备注里

**下分(兑换)备注：** 会显示在兑换查询的描述里

***

## 2. 响应说明

### 2.1 成功响应

```json
{
  "result": 0
}
```

### 2.2 错误响应

```json
{
  "errcode": 212,
  "errmsg": ""
}
```

| 错误码 | 说明                     |
| --- | ---------------------- |
| 212 | 没有这个用户                 |
| 21  | 用户目前处于游戏中，需要退出游戏才能成功扣取 |
| 42  | 扣款失败！用户余额不足            |
| 101 | 参数错误                   |
| 2001 | 用户有投注任务，不能下分 |
| 2002 | 用户没有充值，不能下分         |
| 1   | 服务器内部错误                |

***

## 3. 接口使用示例

### 3.1 上分(充值)示例

```http
POST /admin/offlinepay/offlineopt
Content-Type: application/x-www-form-urlencoded

type=1&uid=123456&amount=10000&mark=线下充值测试
```

### 3.2 下分(兑换)示例

```http
POST /admin/offlinepay/offlineopt
Content-Type: application/x-www-form-urlencoded

type=2&uid=123456&amount=5000&mark=线下兑换测试
```

***

