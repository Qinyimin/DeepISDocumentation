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

### 更新用户信息
|  方法名  |                 updateUserInfo                 |
| :------: | :--------------------------------------------: |
| 传入参数 | 待更新的用户id，更新后的用户名，密码，角色信息 |
|  返回值  |              用户信息是否更新成功              |

```javascript
POST /users/ 
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
GET /users/caseNum
{
    userId: 007,
    total: 100,
    case: [{name:'女性',
    		value:70},
    		{name:'男性',
    		value:30}],
}
```
### 结节数展示
|  方法名  |                totalNodeNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有用户标记结节数量及分布 |

```javascript
GET /users/nodeNum
{
    userId: 007,
    total: 1583,
    case: [	{value: 321, name: '歧义候选淋巴结'},
			{value: 158, name: '结直肠系膜淋巴结'},
			{value: 42, name: '髂外（髂总）淋巴结'},
			{value: 259, name: '髂内近端淋巴结'},
			{value: 30, name: '髂内远端淋巴结'},
			{value: 402, name: '闭孔头测淋巴结'},
			{ value: 117, name: '闭孔尾测淋巴结'},
			{ value: 254, name: '髂总动脉分叉血管淋巴结'}];
```
### 结节数展示
|  方法名  |                totalNodeNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有用户标记结节数量及分布 |

```javascript
GET /users/nodeNum
{
    userId: 007,
    total: 1583,
    case: [	{value: 321, name: '歧义候选淋巴结'},
			{value: 158, name: '结直肠系膜淋巴结'},
			{value: 42, name: '髂外（髂总）淋巴结'},
			{value: 259, name: '髂内近端淋巴结'},
			{value: 30, name: '髂内远端淋巴结'},
			{value: 402, name: '闭孔头测淋巴结'},
			{ value: 117, name: '闭孔尾测淋巴结'},
			{ value: 254, name: '髂总动脉分叉血管淋巴结'}，]
}
```
### 审核数展示
|  方法名  |                totalExamedNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者已标记与已审核数目 |

```javascript
GET /users/examedNum
{
    userId: 007,
    annotated: 50,
    examed: 30,
}
```
### 标注者列表展示
|  方法名  |                getAnnotatorList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者分配标注数量，已标注数量与未标注数量 |

```javascript
GET /users/annotatorList
{
    userId: 007,
    annoList: [{name:'旋涡鸣人'，
    			caseNum:50,
    			annotated:30,
    			unAnnotated:20},
    			......]
}
```
### 标注动态列表展示
|  方法名  |                getAnnotatorActivity                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者的标注动态 |

```javascript
GET /users/annotatorList
{
    userId: 007,
    annoList: [{name:'旋涡鸣人',
				SericeId: '6354132',
				time: '7/10',},
    			......]
}
```

## 病例管理接口
### 标注动态列表展示
|  方法名  |                getCaseList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有病例数据 |

```javascript
GET /users/annotatorList
{
    userId: 007,
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