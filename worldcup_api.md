
# 世界杯活动接口文档

## 1. Excel配置导入

### 1.1 上传Excel配置

**接口地址:** `/admin/worldcup/uploadSubmit`

**请求方法:** POST

**请求参数 (form-data):**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| fileName | string | 是 | 文件名 |
| file | File | 是 | Excel文件 |

---

## 2. 基础配置管理

### 2.1 获取基础配置

**接口地址:** `/admin/worldcup/base/get`

**请求方法:** GET

**请求参数:** 无

**响应示例:**
```json
{
  "start_time": "2024-06-14 00:00:00",
  "end_time": "2024-07-14 23:59:59",
  "min_bet": 100,
  "reward_type": 0,
  "bet_gold": 1,
  "get_reward_type": 0,
  "mail_subject": "世界杯奖励",
  "mail_body": "恭喜您获得世界杯竞猜奖励"
}
```

### 2.2 编辑基础配置

**接口地址:** `/admin/worldcup/base/edit`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| start_time | string | 否 | 开始时间 |
| end_time | string | 否 | 结束时间 |
| min_bet | int64 | 否 | 最低投注金额 |
| reward_type | int | 否 | 奖励类型 0现金 1金币 |
| bet_gold | int | 否 | 打码金币ID |
| get_reward_type | int | 否 | 获取奖励类型 0过期作废 1邮件奖励 |
| mail_subject | string | 否 | 邮件主题 |
| mail_body | string | 否 | 邮件内容 |

---

## 3. 赛事管理

### 3.1 获取赛事列表

**接口地址:** `/admin/worldcup/match/list`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |

**响应示例:**
```json
{
  "total": 100,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "id": 1,
      "date": "2024-06-14",
      "time": "2024-06-14T21:00:00Z",
      "stage": 1,
      "group": 1,
      "home": 1,
      "away": 2,
      "mark": "揭幕战",
      "status": 0,
      "home_score": 0,
      "away_score": 0,
      "created_at": "2024-05-01T00:00:00Z",
      "updated_at": "2024-05-01T00:00:00Z",
      "stage_name": "小组赛",
      "group_name": "A组",
      "home_name": "德国",
      "away_name": "苏格兰"
    }
  ]
}
```

### 3.2 添加赛事

**接口地址:** `/admin/worldcup/match/add`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| date | string | 是 | 日期 |
| time | string | 是 | 时间 |
| stage | int | 是 | 赛段ID |
| group | int | 是 | 组别ID |
| home | int | 是 | 主队ID |
| away | int | 是 | 客队ID |
| mark | string | 否 | 备注名 |

**注意:** 赛事ID会自动生成，无需传递

### 3.3 编辑赛事

**接口地址:** `/admin/worldcup/match/edit`

**请求方法:** POST

**请求参数:** 同添加赛事，id必填用于匹配

### 3.4 删除赛事

**接口地址:** `/admin/worldcup/match/del`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| id | int64 | 是 | 赛事ID |

---

## 4. 赔率管理

### 4.1 获取赔率列表

**接口地址:** `/admin/worldcup/odds/list`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |
| match_id | int64 | 否 | 赛事ID，用于筛选 |

**响应示例:**
```json
{
  "total": 100,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "id": 1,
      "matchid": 1,
      "class1": 1,
      "class2": 1,
      "odds": 1.8,
      "recommend": 0,
      "is_win": 0,
      "created_at": "2024-05-01T00:00:00Z",
      "updated_at": "2024-05-01T00:00:00Z",
      "class1_name": "胜平负",
      "class2_name": "主胜"
    }
  ]
}
```

### 4.2 添加赔率

**接口地址:** `/admin/worldcup/odds/add`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| matchid | int | 是 | 赛事ID |
| class1 | int | 是 | 一级分类ID |
| class2 | int | 是 | 二级分类ID |
| odds | float32 | 是 | 赔率 |
| recommend | int | 否 | 是否推荐，0不推荐 1推荐 |
| is_win | int | 否 | 是否获胜，0未设置 1获胜 2未获胜 |

**注意:** 赔率ID会自动生成，无需传递

### 4.3 编辑赔率

**接口地址:** `/admin/worldcup/odds/edit`

**请求方法:** POST

**请求参数:** 同添加赔率，id必填用于匹配

### 4.4 删除赔率

**接口地址:** `/admin/worldcup/odds/del`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| id | int64 | 是 | 赔率ID |

---

## 5. 比分管理

### 5.1 编辑比赛比分

**接口地址:** `/admin/worldcup/score/edit`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| match_id | int | 是 | 赛事ID |
| home_score | int | 是 | 主队得分 |
| away_score | int | 是 | 客队得分 |
| status | int | 是 | 比赛状态，0未开始 1进行中 2已结束 |

---

## 6. 数据报表

### 6.1 获取数据概况

**接口地址:** `/admin/worldcup/summary`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |
| start_time | string | 否 | 开始时间 |
| end_time | string | 否 | 结束时间 |
| channel | int64 | 否 | 渠道 |
| group_name | string | 否 | 分组名称 |
| home_name | string | 否 | 主队名称 |

**响应示例:**
```json
{
  "total": 100,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "date": "2024-06-14",
      "channel": 10001,
      "match_mark": "揭幕战",
      "stage_name": "小组赛",
      "group_name": "A组",
      "home_name": "德国",
      "away_name": "苏格兰",
      "class1_name": "胜平负",
      "class2_name": "主胜",
      "bet_user_count": 100,
      "bet_amount": 10000,
      "return_amount": 5000
    }
  ]
}
```

### 6.2 下载数据概况

**接口地址:** `/admin/worldcup/summary/download`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始时间 |
| to | string | 是 | 结束时间 |
| channel | int64 | 否 | 渠道 |
| group_name | string | 否 | 分组名称 |
| home_name | string | 否 | 主队名称 |
| fields | array | 否 | 自定义字段 |
| password | string | 是 | 下载密码 |
| bak | string | 否 | 备注 |

**注意:** 时间跨度不能超过30天

### 6.3 获取数据详情

**接口地址:** `/admin/worldcup/detail`

**请求方法:** GET

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| page | int | 否 | 页码，默认1 |
| limit | int | 否 | 每页数量，默认10 |
| start_time | string | 否 | 开始时间 |
| end_time | string | 否 | 结束时间 |
| channel | int64 | 否 | 渠道 |
| uid | int64 | 否 | 用户ID |
| group_name | string | 否 | 分组名称 |
| home_name | string | 否 | 主队名称 |
| action | string | 否 | 行为，"投注"或"结算订单" |

**响应示例:**
```json
{
  "total": 100,
  "curr": 1,
  "limit": 10,
  "list": [
    {
      "bet_time": "2024-06-14T21:00:00Z",
      "channel": 10001,
      "uid": 123456,
      "match_mark": "揭幕战",
      "stage_name": "小组赛",
      "group_name": "A组",
      "home_name": "德国",
      "away_name": "苏格兰",
      "class1_name": "胜平负",
      "class2_name": "主胜",
      "action": "投注",
      "bet_amount": 100
    }
  ]
}
```

### 6.4 下载数据详情

**接口地址:** `/admin/worldcup/detail/download`

**请求方法:** POST

**请求参数:**

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| from | string | 是 | 开始时间 |
| to | string | 是 | 结束时间 |
| channel | int64 | 否 | 渠道 |
| uid | int64 | 否 | 用户ID |
| group_name | string | 否 | 分组名称 |
| home_name | string | 否 | 主队名称 |
| action | string | 否 | 行为 |
| fields | array | 否 | 自定义字段 |
| password | string | 是 | 下载密码 |
| bak | string | 否 | 备注 |

**注意:** 时间跨度不能超过30天

---

## 附录：数据字典

### 比赛状态
- 0: 未开始
- 1: 进行中
- 2: 已结束

### 订单状态
- 0: 未结算
- 1: 赢（可领取）
- 2: 输
- 3: 已领取

### 推荐状态
- 0: 不推荐
- 1: 推荐

### 胜负状态
- 0: 未设置
- 1: 获胜
- 2: 未获胜

### 奖励类型
- 0: 现金
- 1: 金币

### 获取奖励类型
- 0: 过期作废
- 1: 邮件奖励

