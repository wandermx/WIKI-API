#文件管理RestAPI接口说明


此接口为VISSLM提供, 接口实现形式为 HTTP Restful

\*返回值格式默认是"application/json", 本文中使用伪json示意。

URI格式说明

	http://location:port/path?param=value#flag


##获取文件字节数组Base64字符串
---------


URI

		http://<server>/alm/rest/file/GetFileData/fileUrl
**方法:GET**

| 参数 | 说明 |
| --- | :-- |
| fileUrl | 文件链接或文件码 |
| appName | 应用名称 |
| appToken | 应用许可 |

返回值

		{"ErrorCode":0,"ErrorMsg":"成功","Data":"字节数组Base64字符串"}
***


##获取文件属性
---------


URI

		http://<server>/alm/rest/file/GetFileInfo/fileUrl
**方法:GET**

| 参数 | 说明 |
| --- | :-- |
| fileUrl | 文件链接或文件码 |
| appName | 应用名称 |
| appToken | 应用许可 |
| {token} | utoken/apitoken/... |

返回值

		{"ErrorCode":0,"ErrorMsg":"成功","Data":{"FileName":"aa.docx","FileSize":1000,"FileSizeShow":"1000 字节","SecretLevel":-1,"SecretLevelShow":"非密","MD5Code":"AAAAAAAAAAAAAAAAAAAAAAA","DownloadCount":0,"PreviewCount":0,"CreateTime":"2019-10-09","CreateBy":"user","CreateByShow":"演示用户","LastModifyTime":"2019-10-09","LastModifyBy":"user","LastModifyByShow":"演示用户"}}


