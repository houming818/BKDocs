
### 请求方法

GET


### 请求地址

/api/c/compapi/v2/jobv3/get_cron_detail/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

查询定时作业详情

### 请求参数



#### 接口参数

| 字段                   |  类型       | 必选   |  描述       |
|------------------------|------------|--------|------------|
| bk_biz_id              |  long      | 是     | 业务 ID     |
| id                     |  long      | 否     | 定时任务 ID |

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
    "message": "",
    "data": {
        "bk_biz_id": 1,
        "job_plan_id": 100,
        "id": 1,
        "name": "test",
        "status": 1,
        "expression": "0/5 * * * ?",
        "global_var_list": [
            {
                "id": 436,
                "name": "ip",
                "server": {
                    "dynamic_group_list": [
                        {
                            "id": "blo8gojho0skft7pr5q0"
                        },
                        {
                            "id": "blo8gojho0sabc7priuy"
                        }
                    ],
                    "ip_list": [
                        {
                            "bk_cloud_id": 0,
                            "ip": "10.0.0.1"
                        },
                        {
                            "bk_cloud_id": 0,
                            "ip": "10.0.0.2"
                        }
                    ],
                    "topo_node_list": [
                        {
                            "id": 1000,
                            "node_type": "module"
                        }
                    ]
                }
            },
            {
                "id": 437,
                "name": "text",
                "value": "new String value"
            }
        ],
        "creator": "admin",
        "create_time": 1546272000000,
        "last_modify_user": "admin",
        "last_modify_time": 1577807999999
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
| 字段             | 类型      | 描述      |
|------------------|-----------|-----------|
| bk_biz_id        | long      | 业务 ID |
| job_plan_id      | long      | 执行方案 ID |
| id               | long      | 定时作业 ID |
| name             | string    | 定时作业名称 |
| status           | int       | 定时作业状态：1.已启动、2.已暂停 |
| expression       | string    | 定时任务 crontab 的定时规则，新建时必填，修改时选填。各字段含义为：分 时 日 月 周，如: 0/5 * * * ? 表示每 5 分钟执行一次 |
| global_var_list |  array     | 全局变量信息 |
| creator          | string    | 作业创建人帐号 |
| create_time      | long      | 创建时间，Unix 时间戳 |
| last_modify_user | string    | 作业修改人帐号 |
| last_modify_time | long      | 最后修改时间，Unix 时间戳 |

#### global_var

| 字段       |  类型     |  描述      |
|-----------|-----------|------------|
| id        |  long     | 全局变量 id，唯一标识。如果 id 为空，那么使用 name 作为唯一标识 |
| name      |  string   | 全局变量 name |
| value     |  string   | 字符、密码、数组类型的全局变量的值 |
| server    |  object   | 主机类型全局变量的值 |

#### server
| 字段                   |  类型 |  描述      |
|-----------------------|-------|------------|
| ip_list               | array | 静态 IP 列表 |
| dynamic_group_list | array | 动态分组 列表 |
| topo_node_list        | array | 动态 topo 节点列表 |

#### ip

| 字段         |  类型   |  描述   |
|-------------|---------|---------|
| bk_cloud_id |  int    | 云区域 ID |
| ip          |  string | IP 地址 |

#### topo_node
| 字段              |  类型  |  描述      |
|------------------|--------|------------|
| id               | long   | 动态 topo 节点 ID，对应 CMDB API 中的 bk_inst_id |
| node_type        | string | 动态 topo 节点类型，对应 CMDB API 中的 bk_obj_id,比如"module","set"|