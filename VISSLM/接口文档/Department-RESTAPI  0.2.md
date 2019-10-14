#部门管理RestAPI接口说明


此接口为VISSLM提供, 接口实现形式为 HTTP Restful

\*返回值格式默认是"application/json", 本文中使用伪json示意。

URI格式说明

	http://location:port/path?param=value#flag


##获取部门信息
---------


URI

		http://<server>/alm/rest/department/{d-name}/
**方法:GET**

|参数 | 说明 |
| --- | :-- |
| {d-name} | 部门名称 |
| AppName | 应用名称 |
| AppToken | 应用许可 |

返回值

	{"ErrorCode":0,"ErrorMsg":"成功",
		"Data":{
			"UID":6,
			"ParentID":2,
			"Name":"研发部",			
			"Description":"xxx",
			"Code":"RD",
			"CellPhones":"3322222",
			...
			}
	}
***


##获取子部门信息
---------


URI

		http://<server>/alm/rest/department/{d-name}/sub

**方法:GET**

| 参数 | 说明 |
| --- | :-- |
| {d-name} | 部门名称 |
| AppName | 应用名称 |
| AppToken | 应用许可 |

返回值

		{
			"ErrorCode":0,"ErrorMsg":"成功",
			"Data":	[
					{
						"UID":7,"Name":"研发部1",
						...
					},
					{
						"UID":8,"Name":"研发部2",
						...
					}
			]
		}
***

##修改部门信息
---------

修改部门信息

URI

		http://<server>/alm/rest/department/{d-name}/

**方法:PUT**

| 参数 | 说明 |
| --- | :-- |
| {d-name} | 部门名称 |
| AppName | 应用名称 |
| AppToken | 应用许可 |

Content

	{
		"Description":"Desc",
		"Code":"2222"
	}

返回值

	{
		"ErrorCode":0,"ErrorMsg":"成功"
	}

***


##增加子部门
---------
可同时增加多个

URI

		http://<server>/alm/rest/department/{d-name}/

**方法:POST**

| 参数 | 说明 |
| --- | :-- |
| {d-name} | 部门名称 |
| AppName | 应用名称 |
| AppToken | 应用许可 |

Content

	[
		{
			"Name" : "NewSub1",
			"Description":"Desc",
			"Code":"2222"
		}，
		{}
	]

返回值

	{
		"ErrorCode":0,"ErrorMsg":"成功"，
		"Data":{
			"SuccessAdd":[]，
			"FailAdd":[]
		}
	}

***


##删除部门
---------


URI

		http://<server>/alm/rest/department/{d-name}/

**方法:DELETE**

返回值

	{
		"ErrorCode":0,"ErrorMsg":"成功"，
		"Data":{
			"SuccessAdd":[]，
			"FailAdd":[]
		}
	}

***

##查询部门成员
---------


URI

		http://<server>/alm/rest/department/{d-name}/member

**方法:GET**


返回值


	{
		"ErrorCode":0,"ErrorMsg":"成功"，
		"Data":[
			{
				"Name":"user"，
				"NickName":"演示用户"
			}
		]
	}
***

##增加部门成员
---------
可增加多个用户, 并可设置为部门负责人

URI

		http://<server>/alm/rest/department/{d-name}/assignment/append

**方法:POST**

Content
	{
		"member":["SA",...],
		"admin": ["SA"]
	}

返回值
	{
		"ErrorCode":0,"ErrorMsg":"成功"，
	}
***

##删除部门成员
---------


URI

		http://<server>/alm/rest/department/{d-name}/assignment/remove

**方法:POST**

Content
	{
		"member":["SA",...]
	}

返回值
	{
		"ErrorCode":0,"ErrorMsg":"成功"，
	}
***


##替换部门成员
---------
此方法与增加部门成员的区别是，会清空原有部门成员

URI

		http://<server>/alm/rest/department/{d-name}/assignment/replace

**方法:POST**

Content
	{
		"member":["SA",...],
		"admin": ["SA"]
	}

返回值

	{
		"ErrorCode":0,"ErrorMsg":"成功"，
	}

***


				
				