
### 请求方法

GET


### 请求地址

/api/c/compapi/v2/jobv3/get_script_version_detail/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

查询业务脚本版本详情

### 请求参数



#### 接口参数

| 字段       |  类型      | 必选   |  描述      |
|----------------------|------------|--------|------------|
| bk_biz_id      |  long       | 是     | 业务 ID |
| id             |  long       | 是     | 脚本版本 ID，若传入则以此条件为准屏蔽其他条件 |
| script_id      |  string     | 否     | 脚本 ID（可与 version 一起传入定位某个脚本版本）  |
| version        |  string     | 否     | 脚本版本（可与 script_id 一起传入定位某个脚本版本） |

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": 1,
    "id": 1
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "id": 1,
        "bk_biz_id": 1,
        "script_id": "000dbdddc06c453baf1f2decddf00c69",
        "version": "V1.0",
        "content": "#!/bin/bash***",
        "status": 1,
        "version_desc": "版本描述",
        "creator": "admin",
        "create_time": 1600746078520,
        "last_modify_user": "admin",
        "last_modify_time": 1600746078520
    }
}
```

### 返回结果参数说明

#### response
| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| result       | bool   | 请求成功与否。true:请求成功；false 请求失败 |
| code         | int    | 错误编码。 0 表示 success，>0 表示失败错误 |
| message      | string | 请求失败返回的错误信息|
| data         | object | 请求返回的数据|
| permission   | object | 权限信息|
| request_id   | string | 请求链 id|

#### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| id                | long      | 脚本版本 ID |
| bk_biz_id         | long      | 业务 ID |
| script_id         | string    | 脚本版本所属的脚本 ID |
| version           | string    | 版本号 |
| content           | string    | 脚本版本内容 |
| status            | int       | 脚本版本状态（0：未上线，1：已上线，2：已下线，3：已禁用） |
| version_desc      | string    | 版本描述  |
| creator           | string    | 创建人 |
| create_time       | long      | 创建时间 Unix 时间戳（ms） |
| last_modify_user  | string    | 最近一次修改人 |
| last_modify_time  | long      | 最近一次修改时间 Unix 时间戳（ms） |