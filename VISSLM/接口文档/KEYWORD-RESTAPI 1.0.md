#对象关键字RestAPI接口说明


此接口为VISSLM提供, 接口实现形式为 HTTP Restful

\*返回值格式默认是"application/json", 本文中使用伪json示意。

URI格式说明

	http://location:port/path?param=value#flag


##获取项目内关键字统计情况
---------


URI

		http://<server>/alm/rest/keyword/GetKeyWordStatistics

**方法:GET**

| 参数 | 类型 | 是否必填 | 说明 |
| --- | :-- | :-- | :-- |
| proId | string | 是 | 项目id |
| number | int | 否 | 关键字数量，默认返回10个 |
| {token} | string | 是 | utoken/apitoken/apptoken/... |

返回值

		{"ErrorCode":0,"ErrorMsg":"成功","Data":[{"KeyText":"tag","Count":1}]}
***


		


