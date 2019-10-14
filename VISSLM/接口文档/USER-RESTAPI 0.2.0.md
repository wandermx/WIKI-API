#用户RestAPI接口说明


此接口为VISSLM提供, 接口实现形式为 HTTP Restful

\*返回值格式默认是"application/json", 本文中使用伪json示意。

URI格式说明

	http://location:port/path?param=value#flag


##用户登录
---------

此为内部临时接口,随时取消

URI

		http://<server>/alm/rest/user/login/{user}/{password}
**方法:GET**

|参数 | 说明 |
| --- | :-- |
| {user} | 用户登录名 |
| {password} | 用户密码 |

返回值

		{"ErrorCode":0,"ErrorMessage":null,"props":{"UToken":"UT4ce88ac904f04920b4746c9e786c54b7"}}
***


##获取用户信息
---------

根据令牌获取用户信息，此为内部临时接口,可能取消

URI

		http://<server>/alm/rest/user/info/{utoken}
**方法:GET**

|参数 | 说明 |
| --- | :-- |
| {utoken} | 用户身份令牌 |

返回值

		{
		 "AppName":"VISSLM_MAIN","GroupIds":"88,130,58,137,145","IP":"192.168.0.106","LicenseType":0,
		 "NickName":"武则天","UToken":"UT4ce88ac904f04920b4746c9e786c54b7","Uid":170,"UserName":"Wu","UserType":0
		}
***

##获取许可信息
---------

获取当前许可服务信息

URI

		http://<server>/alm/rest/user/LicenseInfo
**方法:GET**


返回值

	{
		"Float":{"ExpirationType":0,"MaxUserCount":2,"ExpiresTime":60,"TokenList":{}},
		"Static":{"ExpirationType":0,"ExpiresTime":60,"MaxUserCount":500,"TokenList"：{}}
	}
***


##获取用户的API令牌
---------

获取指定用户的API令牌, 此为内部临时接口,可能取消

URI

		http://<server>/alm/rest/user/ApiToken/{utoken}
**方法:GET**


返回值

	{"ErrorCode":0,"props":{"apiToken","Aadfasdfasgljksjdfsddasfasdffklss"}}
***


##获取第三方登录会话句柄
---------

获取第三方登录会话句柄, 供后续接口使用

URI

		http://<server>/alm/rest/user/TPL/session/{appName}
**方法:GET**


返回值

	{"ErrorCode":0,"props":{"TPLSession","Aadfasdfasgljksjdfsddasfasdffklss"}}
***

##查询第三方登录授权状态
---------

使用之前获取的第三方登录会话句柄, 查询第三方登录授权状态

URI

		http://<server>/alm/rest/user/TPL/CheckAuth/{TPLSession}
**方法:GET**


返回值

	{"ErrorCode":0,"props":{"UToken","Aadfasdfasgljksjdfsddasfasdffklss"}}
***

##第三方验证用户登录
---------

使用之前获取的第三方登录会话句柄, 发送VISSLM用户登录名信息，进行第三方用户登录

URI

		http://<server>/alm/rest/user/TPL/login/{TPLSession}

**方法:GET**


返回值

	{"ErrorCode":0}
***




				
				