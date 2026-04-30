# 首充礼盒管理接口文档

## 1. 首充礼盒数据汇总

### 1.1 获取数据汇总

**接口地址:** `/admin/firstpaybox/summary`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始日期，格式: 2006-01-02 |
| to | string | 是 | 结束日期，格式: 2006-01-02 |
| channel | int | 否 | 渠道ID，默认0表示全部 |
| gift_type | int | 否 | 参与类型，0-所有，1-首充，2-二充，3-三充 |

**响应示例:**

```json
{
  "first_pay": {
    "users_num": 5000,
    "recharge_amount": 2000.00,
    "cash_amount": 2000.00,
    "gold_amount": 5000.00,
    "bonus_amount": 6000.00
  },
  "second_pay": {
    "users_num": 5000,
    "recharge_amount": 2000.00,
    "cash_amount": 2000.00,
    "gold_amount": 5000.00,
    "bonus_amount": 6000.00
  },
  "third_pay": {
    "users_num": 5000,
    "recharge_amount": 2000.00,
    "cash_amount": 2000.00,
    "gold_amount": 5000.00,
    "bonus_amount": 6000.00
  }
}
```

**响应字段说明:**

| 字段名 | 类型 | 说明 |
|--------|------|------|
| first_pay.users_num | int | 首充人数 |
| first_pay.recharge_amount | float | 首充充值金额 |
| first_pay.cash_amount | float | 首充现金发放 |
| first_pay.gold_amount | float | 首充金币发放 |
| first_pay.bonus_amount | float | 首充BONUS发放 |
| second_pay.* | - | 二充统计，字段同上 |
| third_pay.* | - | 三充统计，字段同上 |

---

## 2. 首充礼盒数据概况列表

### 2.1 获取数据概况列表

**接口地址:** `/admin/firstpaybox/summarydata`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始日期，格式: 2006-01-02 |
| to | string | 是 | 结束日期，格式: 2006-01-02 |
| channel | int | 否 | 渠道ID，默认0表示全部 |
| gift_type | int | 否 | 参与类型，0-所有，1-首充，2-二充，3-三充 |
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |

**响应示例:**

```json
{
  "total": 60,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "day": "2026-06-06",
      "channel": 2010001,
      "type": "首充",
      "gift_box_id": 10001,
      "users_num": 999,
      "recharge_amount": 9990.00,
      "cash_amount": 9990.00,
      "gold_amount": 9990.00,
      "bonus_amount": 9990.00
    }
  ]
}
```

**响应字段说明:**

| 字段名 | 类型 | 说明 |
|--------|------|------|
| day | string | 日期 |
| channel | int | 渠道ID |
| type | string | 参与类型(首充/二充/三充) |
| gift_box_id | int | 礼盒ID |
| users_num | int | 参与人数 |
| recharge_amount | float | 充值金额 |
| cash_amount | float | 现金发放 |
| gold_amount | float | 金币发放 |
| bonus_amount | float | BONUS发放 |

### 2.2 导出数据概况列表

**接口地址:** `/admin/firstpaybox/downloadsummarydata`

**请求方法:** POST

**请求参数 (JSON):**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始日期，格式: 2006-01-02 |
| to | string | 是 | 结束日期，格式: 2006-01-02 |
| channel | int | 否 | 渠道ID，默认0表示全部 |
| gift_type | int | 否 | 参与类型，0-所有，1-首充，2-二充，3-三充 |
| fields | array | 是 | 导出字段配置 |
| bak | int | 是 | 备注标识 |
| password | string | 是 | 下载密码 |

**响应示例:**

```json
{
  "file_name": "FirstPayBoxSummaryData_20260101_120000.xlsx"
}
```

---

## 3. 首充礼盒明细数据

### 3.1 获取明细数据列表

**接口地址:** `/admin/firstpaybox/list`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始日期，格式: 2006-01-02 |
| to | string | 是 | 结束日期，格式: 2006-01-02 |
| uid | int | 否 | 用户ID，默认0表示全部 |
| gift_type | int | 否 | 参与类型，0-所有，1-首充，2-二充，3-三充 |
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |

**响应示例:**

```json
{
  "total": 60,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "id": 1,
      "uid": 20260606,
      "channel": 2010001,
      "day": "2026-06-06",
      "type": 1,
      "gift_box_id": 10001,
      "recharge_amount": 999.00,
      "cash_amount": 9990.00,
      "gold_amount": 9990.00,
      "bonus_amount": 9990.00,
      "created_at": "2026-06-06 12:00:00"
    }
  ]
}
```

**响应字段说明:**

| 字段名 | 类型 | 说明 |
|--------|------|------|
| id | int | 记录ID |
| uid | int | 用户ID |
| channel | int | 渠道ID |
| day | string | 日期 |
| type | int | 参与类型，1-首充，2-二充，3-三充 |
| gift_box_id | int | 礼盒ID |
| recharge_amount | float | 充值金额 |
| cash_amount | float | 现金发放 |
| gold_amount | float | 金币发放 |
| bonus_amount | float | BONUS发放 |
| created_at | string | 创建时间 |

### 3.2 导出明细数据

**接口地址:** `/admin/firstpaybox/downloadfirstpaybox`

**请求方法:** POST

**请求参数 (JSON):**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始日期，格式: 2006-01-02 |
| to | string | 是 | 结束日期，格式: 2006-01-02 |
| uid | int | 否 | 用户ID，默认0表示全部 |
| channel | int | 否 | 渠道ID，默认0表示全部 |
| gift_type | int | 否 | 参与类型，0-所有，1-首充，2-二充，3-三充 |
| fields | array | 是 | 导出字段配置 |
| bak | int | 是 | 备注标识 |
| password | string | 是 | 下载密码 |

**响应示例:**

```json
{
  "file_name": "FirstPayBox_20260101_120000.xlsx"
}
```

---

## 4. 错误响应

所有接口在发生错误时返回统一格式：

```json
{
  "code": 错误码,
  "msg": "错误信息"
}
```

## 5. 说明

- 所有金额字段单位为元（保留两位小数）
- 日期格式统一为 `2006-01-02`
- 导出接口需要验证下载密码
