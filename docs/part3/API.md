[TOC]

# 前后端API定义

## 说明
本文档是智能肠胃组前端和后端之间数据接口的定义。文档中提供的方法名为系统前端接口的名称，供后端系统编写人员参考。以get开头的函数名表示该函数使用HTTP GET方法。接口返回值一律使用JSON格式的数据。接口暂时省略访问信息时的身份验证过程。每个代码片中展示了该接口的一个示例，传入参数和期望的返回值之间用空行分隔。示例只展示请求成功应该返回的结果；如果请求失败，要求返回404状态码。
## 用户信息接口
### 登录验证
|  方法名  |                loginValidation                 |
| :------: | :--------------------------------------------: |
| 传入参数 |        用户在登录表单输入的用户名和密码        |
|  返回值  | 如果数据库中存在匹配的用户名和密码返回用户信息 |

```javascript
POST /users/login
{
    username: "qin",
    password: "111" /* 待加密 */
}

{
    userId: 007,
    username: "qin",
    password: "111", /* 待加密 */
    roles: [roleId1, roleId2, ...],
}
```

### 获取单个用户信息
|  方法名  |         getUserInfo          |
| :------: | :--------------------------: |
| 传入参数 |            用户id            |
|  返回值  | 与该用户id匹配的用户全部信息 |

```javascript
GET /users/{userId}

{
    userId: 001,
    username: "admin",
    password: "admin",
    roles: [roleId1, roleId2, ...],
}
```

### 获取全部用户信息

|  方法名  |        getAllUsersInfo         |
| :------: | :----------------------------: |
| 传入参数 |               -                |
|  返回值  | 一个包含系统所有用户信息的列表 |

```javascript
GET /users

[
    {
        userID: 001,
        username: "admin",
        password: "admin",
        roles: [roleId1, roleId2, ...]
    },
    ...
]
```

### 添加用户信息
|  方法名  |        addUser        |
| :------: | :-------------------------: |
| 传入参数 | 待添加的用户名，密码，角色信息 |
|  返回值  | 用户信息是否添加成功  |

```javascript
POST /users
{
    username: "qin", 
    password: "111",
    roles: [roleId1, roleId2, ...]
}

Status: 200
```

### 更新用户信息

|  方法名  |                 updateUserInfo                 |
| :------: | :--------------------------------------------: |
| 传入参数 | 待更新的用户id，更新后的用户名，密码，角色信息 |
|  返回值  |              用户信息是否更新成功              |

```javascript
POST /users/{userId}
{
    userId: 007,
    username: "qin", 
    password: "111",
    roles: [roleId1, roleId2, ...]
}

Status: 200
```

### 删除用户信息
|  方法名  |    deleteUserInfo    |
| :------: | :------------------: |
| 传入参数 |    待删除的用户Id    |
|  返回值  | 用户信息是否删除成功 |

```javascript
DELETE /users/{userId}

Status: 200
```
## 角色信息接口
### 获取单个角色信息
|  方法名  | getRoleInfoById |
| :------: | :-------------: |
| 传入参数 |   用户角色id    |
|  返回值  |  用户角色信息   |

```javascript
GET /roles/{roleId}

{
    roleId: 001,
    roleName: "管理员",
    roleDescription: "拥有全部权限的管理员",
    rolePowers: [powerId1, powerId2,...]
}
```

### 获取全部角色信息
|  方法名  | getAllRoles  |
| :------: | :----------: |
| 传入参数 |      -       |
|  返回值  | 全部角色信息 |

```javascript
GET /roles

[
    {
        roleId: 001,
    	roleName: "管理员",
    	roleDescription: "拥有全部权限的管理员",
    	rolePowers: [powerId1, powerId2,...]
    },
    ...
]
```

### 添加角色信息
|  方法名  |      addRole      |
| :------: | :----------------------: |
| 传入参数 | 待添加的角色信息 |
|  返回值  |  角色信息是否添加成功  |

```javascript
POST /roles
{
    roleName: "二级审核者",
    roleDescription: "对已审核过的数据再次进行审核",
    rolePowers: [powerId1, powerId2,...]
}

Status 200
```

### 修改角色信息
|  方法名  |      updateRoleInfo      |
| :------: | :----------------------: |
| 传入参数 | 角色id，更新后的角色信息 |
|  返回值  |   角色信息是否修改成功   |

```javascript
POST /roles/{roleId}
{
    roleId: 001,
    roleName: "管理员",
    roleDescription: "拥有全部权限的管理员",
    rolePowers: [powerId1, powerId2,...]
}

Status 200
```
### 删除角色信息
|  方法名  |    deleteRoleInfo    |
| :------: | :------------------: |
| 传入参数 |        角色id        |
|  返回值  | 角色信息是否删除成功 |

```javascript
DELETE /roles/{roleId}

Status 200
```

## 权限信息接口
### 获取单个权限信息
|  方法名  | getPowerInfoById |
| :------: | :--------------: |
| 传入参数 |    用户权限id    |
|  返回值  |   用户权限信息   |

```javascript
GET /powers/{powerId}

{
    powerId: 004,
    powerName: "删除用户",
    powerCode: "user:delete",
}
```

### 获取全部权限信息
|  方法名  |    getAllPowers    |
| :------: | :----------------: |
| 传入参数 |         -          |
|  返回值  | 全部用户的角色信息 |

```javascript
GET /powers

[
    {
        powerId: 001,
        powerName: "查看用户",
        powerCode: "user:view",
    },
    {...},
    ...
]
```
## 展示信息接口
### 病例数展示
|  方法名  |                totalCaseNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有用户数量及分布 |

```javascript
GET /cases/caseNum/{userId, keywords}
{
    total: 100,
    case: [{"gender":"女",
    		"value":70},
    		{"gender":"男",
    		"value":30}],
}
```
### 结节数展示
|  方法名  |                totalNodeNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有用户标记结节数量及分布 |

```javascript
GET /measurements/nodeNum/{userId}
{
    total: 1583,
    case: [	{value: 321, "partition": '歧义候选淋巴结'},
			{value: 158, "partition": '结直肠系膜淋巴结'},
			{value: 42, "partition": '髂外（髂总）淋巴结'},
			{value: 259, "partition": '髂内近端淋巴结'},
			{value: 30, "partition": '髂内远端淋巴结'},
			{value: 402, "partition": '闭孔头测淋巴结'},
			{value: 117, "partition": '闭孔尾测淋巴结'},
			{value: 254, "partition": '髂总动脉分叉血管淋巴结'}，]
}
```
### 标注者列表展示
|  方法名  |                getAnnotatorList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者已标注数量,已审核数量,未标注数量 |

```javascript
GET /cases/getAnnotatorList/{userId}
{
    [{  name:'旋涡鸣人'，
        annotated:30,
        examed: 14,
        unAnnotated:20},
        ......]
}
```
### 病例标注情况列表展示
|  方法名  |                getExamedList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        标注者id        |
|  返回值  | 标注者分配病例及其标注与审核情况 |

```javascript
GET /cases/getExamedList/{userId}
{
    annoList: [{    PatientName: 'Li gang',
                    MRN: '0009629786',
                    AccessionNumber: 'CT00566598',
                    IsAnnotated: 'yes',
                    IsExamed: 'yes',
                    StudyDate: '6月20, 2013',
                    AnnotatedNodeNumbers: '68',
                    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835',
                    key:'1.2.840.78.75.7.5.1674158.1371717835'
                }, {
                    PatientName: 'Wu Yanzu',
                    MRN: '0009629786',
                    AccessionNumber: 'CT00566598',
                    IsAnnotated: 'yes',
                    IsExamed: null,
                    StudyDate: '6月20, 2013',
                    AnnotatedNodeNumbers: '79',
                    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717836',
                    key: '1.2.840.78.75.7.5.1674158.1371717836',
                }
    			......]
(IsAnnotated表示该病例是否被标注（'yes'/null），IsExamed表示该病例是否被审核（'yes'/null）)                
}
```
### 标注动态列表展示
|  方法名  |                getAnnotatorActivity                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者的标注动态 |

```javascript
GET /users/getAnnotatorActivity/{userId}
{
    annoList: [{name:'旋涡鸣人',
				SericeId: '6354132',
				time: '7/10',},
    			......]
}
```

## 病例管理接口
### 病例列表展示
|  方法名  |                getCaseList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有病例数据 |

```javascript
GET /cases/annotatorList/{userId}
{

    caseList: [{PatientName: 'Li gang', 
				MRN: '0009629786', 
				AccessionNumber: 'CT00566598', 
				Modality: 'CT', 
				StudyDate: '6月20, 2013', 
				StudyDescription:'Abdomen^HX_ch_abd_c(Adult)',
				StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835',},
				{…….}
}
(StudyInstanceUID用于跳转ohif相应病例,不可缺少，其余为展示内容，可按情况增减)
```
## 结节搜索接口接口
### 搜索结果展示
|  方法名  |                getNodeList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        结节搜索条件（分区、直径）       |
|  返回值  | 满足条件的结节列表 |

```javascript
POST /measurements/nodeList
{
    partition:'XM',
    diam: [1.0, 1.5],
    caseList: [ PationtName:'Li gang',
                diam: 1.3,
                partition: 'XM',
                ....],
				{…….}
}
(搜索满足分区'为结直肠系膜淋巴结'(XM),直径在1.0~1.5cm范围内的结节 )
```