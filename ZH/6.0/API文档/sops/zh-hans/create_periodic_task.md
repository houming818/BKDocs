
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/sops/create_periodic_task/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

创建周期任务

### 请求参数

#### 接口参数

| 字段          |  类型       | 必选   |  描述             |
|---------------|------------|--------|------------------|
|   template_id    |   string     |   是   |  用于创建任务的模板ID |
| template_source | string   | 否     | 流程模板来源，business:默认值，业务流程，common：公共流程 |
|   bk_biz_id    |   string     |   是   |  任务所属业务ID |
|   name    |   string     |   是   |  要创建的周期任务名称 |
|   cron    |   dict     |   是   |  要创建的周期任务调度策略 |
|   constants    |   dict     |   否   | 任务全局参数，详细信息见下面说明 |
|   exclude_task_nodes_id    |   list     |   否   |  跳过执行的节点ID列表 |
| scope | string | 否 | bk_biz_id 检索的作用域。默认为 cmdb_biz，此时检索的是绑定的 CMDB 业务 ID 为 bk_biz_id 的项目；当值为 project 时则检索项目 ID 为 bk_biz_id 的项目|

#### constants KEY

变量 KEY，${key} 格式

#### constants VALUE

变量值

#### cron

|   参数名称   |    参数类型  |  必须  |     参数说明     |
| ------------ | ------------ | ------ | ---------------- |
|   minute    |   string     |   否   |  分，默认为 * |
|   hour    |   string     |   否   |  时，默认为 * |
|   day_of_week    |   string     |   否   |  一周内的某些天，默认为 * |
|   day_of_month    |   string     |   否   |  一个月中的某些天，默认为 * |
|   month_of_year    |   string     |   否   |  一年中的某些月份，默认为 * |

### 请求参数示例

```
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_username": "xxx",
    "template_id": "1",
    "bk_biz_id": "2",
    "template_source": "business",
	"name": "from api 3",
	"cron" : {
	    "minute": "*/1", 
	    "hour": "15", 
	    "day_of_week":"*", 
	    "day_of_month":"*", 
	    "month_of_year":"*"
    },
	"constants": {
	    "${bk_timing}": "100"
    },
	"exclude_task_nodes_id": ["nodea5c396a3ef0f9f3cd7d4d7695f78"],
	"scope":"cmdb_biz"
}
```

### 返回结果示例

```
{
    "message": "",
    "data": {
        "cron": "*/1 15 * * * (m/h/d/dM/MY)",
        "total_run_count": 0,
        "name": "from api 3",
        "form": {
            "${bk_timing}": {
                "source_tag": "sleep_timer.bk_timing",
                "source_info": {
                    "node76393dcfedcf73dbc726f1c4786d": [
                        "bk_timing"
                    ]
                },
                "name": "定时时间",
                "index": 0,
                "custom_type": "",
                "value": "100",
                "show_type": "show",
                "source_type": "component_inputs",
                "key": "${bk_timing}",
                "validation": "",
                "desc": ""
            }
        },
        "creator": "admin",
        "pipeline_tree": {
            "activities": {
                "node76393dcfedcf73dbc726f1c4786d": {
                    "outgoing": "linecf7b7f10c87187a88b72c5f91177",
                    "incoming": "linecd597f19606c1455d661f71a582d",
                    "name": "定时",
                    "error_ignorable": false,
                    "component": {
                        "code": "sleep_timer",
                        "data": {
                            "bk_timing": {
                                "hook": true,
                                "value": "${bk_timing}"
                            }
                        }
                    },
                    "stage_name": "步骤1",
                    "optional": false,
                    "type": "ServiceActivity",
                    "id": "node76393dcfedcf73dbc726f1c4786d",
                    "loop": {}
                }
            },
            "end_event": {
                "incoming": "linecf7b7f10c87187a88b72c5f91177",
                "outgoing": "",
                "type": "EmptyEndEvent",
                "id": "node375320830be9c46cd89f4069857d",
                "name": ""
            },
            "outputs": [],
            "flows": {
                "linecd597f19606c1455d661f71a582d": {
                    "is_default": false,
                    "source": "node4e87796ddd76b0d59337b08f385d",
                    "id": "linecd597f19606c1455d661f71a582d",
                    "target": "node76393dcfedcf73dbc726f1c4786d"
                },
                "linecf7b7f10c87187a88b72c5f91177": {
                    "is_default": false,
                    "source": "node76393dcfedcf73dbc726f1c4786d",
                    "id": "linecf7b7f10c87187a88b72c5f91177",
                    "target": "node375320830be9c46cd89f4069857d"
                }
            },
            "gateways": {},
            "line": [
                {
                    "source": {
                        "id": "node4e87796ddd76b0d59337b08f385d",
                        "arrow": "Right"
                    },
                    "id": "linecd597f19606c1455d661f71a582d",
                    "target": {
                        "id": "node76393dcfedcf73dbc726f1c4786d",
                        "arrow": "Left"
                    }
                },
                {
                    "source": {
                        "id": "node76393dcfedcf73dbc726f1c4786d",
                        "arrow": "Right"
                    },
                    "target": {
                        "id": "node375320830be9c46cd89f4069857d",
                        "arrow": "Left"
                    },
                    "id": "linecf7b7f10c87187a88b72c5f91177"
                }
            ],
            "start_event": {
                "incoming": "",
                "outgoing": "linecd597f19606c1455d661f71a582d",
                "type": "EmptyStartEvent",
                "id": "node4e87796ddd76b0d59337b08f385d",
                "name": ""
            },
            "constants": {
                "${bk_timing}": {
                    "source_tag": "sleep_timer.bk_timing",
                    "source_info": {
                        "node76393dcfedcf73dbc726f1c4786d": [
                            "bk_timing"
                        ]
                    },
                    "name": "定时时间",
                    "index": 0,
                    "custom_type": "",
                    "value": "100",
                    "show_type": "show",
                    "source_type": "component_inputs",
                    "key": "${bk_timing}",
                    "validation": "",
                    "desc": ""
                }
            },
            "location": [
                {
                    "y": 150,
                    "x": 80,
                    "type": "startpoint",
                    "id": "node4e87796ddd76b0d59337b08f385d"
                },
                {
                    "y": 149,
                    "x": 1092,
                    "type": "endpoint",
                    "id": "node375320830be9c46cd89f4069857d"
                },
                {
                    "stage_name": "步骤1",
                    "name": "定时",
                    "y": 133,
                    "x": 300,
                    "type": "tasknode",
                    "id": "node76393dcfedcf73dbc726f1c4786d"
                }
            ]
        },
        "last_run_at": "",
        "enabled": false,
        "id": 11,
        "template_id": 2,
        "template_source": "business"
    },
    "result": true,
    "request_id": "xxx",
    "trace_id": "xxx"
}
```

### 返回结果参数说明

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  result      |    bool    |      true/false 操作是否成功     |
|  data        |    dict      |      result=true 时成功数据，详细信息请见下面说明     |
|  message        |    string      |      result=false 时错误信息     |
|  request_id     |    string  |      esb 请求 id     |
|  trace_id     |    string  |      open telemetry trace_id     |

#### data

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  cron      |    string    |      周期调度表达式    |
|  total_run_count      |    int    |    周期任务运行次数   |
|  name      |    string    |    周期任务名   |
|  creator      |    string    |    创建者   |
|  last_run_at      |    string    |    上次运行时间   |
|  enabled      |    bool    |    是否激活   |
|  id      |    int    |    周期任务 ID   |
|  template_id      |    string    |    用于创建该任务的模板 ID   |
| template_source | string    | 流程模板来源，business:默认值，业务流程，common：公共流程 |
|  form      |    dict    |    该周期任务的参数表单对象   |
|  pipeline_tree      |    dict    |    该周期任务的实例树   |

#### data.pipeline_tree

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  start_event      |    dict    |      开始节点信息     |
|  end_event      |    dict    |      结束节点信息    |
|  activities      |    dict    |      任务节点（标准插件和子流程）信息    |
|  gateways      |    dict    |      网关节点（并行网关、分支网关和汇聚网关）信息    |
|  flows      |    dict    |     顺序流（节点连线）信息    |
|  constants      |    dict    |  全局变量信息，详情见下面    |
|  outputs      |    list    |  模板输出信息，标记 constants 中的输出字段    |

#### data.form KEY, data.pipeline_tree.constants KEY

全局变量 KEY，${key} 格式

#### data.form VALUE, data.pipeline_tree.constants VALUE

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  key      |    string    |      同 KEY     |
|  name      |    string    |      变量名字    |
|  index      |    int    |      变量在模板中的显示顺序    |
|  desc      |    string    |      变量说明   |
|  source_type      |    string    |      变量来源, 取值范围 custom: 自定义变量，component_inputs: 从标准插件输入参数勾选，component_outputs：从标准插件输出结果中勾选   |
|  custom_type      |    string    |      source_type=custom 时有效，自定义变量类型， 取值范围 input: 输入框，textarea: 文本框，datetime: 日期时间，int: 整数|
|  source_tag      |    string    |      source_type=component_inputs/component_outputs 时有效，变量的来源标准插件   |
|  source_info   |   dict  |  source_type=component_inputs/component_outputs 时有效，变量的来源节点信息 |