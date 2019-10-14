#配置管理工具(适配器)RestAPI接口说明 V2.1


此接口为所有版本工具适配器公用, 包括VISSLM本身. 接口实现形式为 HTTP Restful

\*返回值格式默认是"application/json", 本文中使用伪json示意。

URI格式说明

	http://user:password@location:port/path?param=value#flag


##项目配置库容器(for VISSLM)
----------

项目中的配置项资源, 可列出项目中的三库资源，utoken为授权令牌

URI

		http://<server>/alm/rest/cm/project/{pid}/library?UToken={utoken}
**方法:GET**

返回值

		[ {type:"librarytype”, “name":"开发库","resource":"\<CM-URI\>"} ,… ] 
***


##配置项容器(for VISSLM)
----------
项目中的配置项资源, 可列出项目中所有的配置项资源，pid为项目ID, type为库类型,utoken为授权令牌

URI

		http://<server>/alm/rest/cm/project/<pid>/ci
		http://<server>/alm/rest/cm/project/{pid}/library/{type}/?UToken={utoken}

方法:GET

返回值

		[ {type:"ci", "name":"任务书","resource":"\<CI-URI\>",”id”:”108”,”item-id”:”PRJ-CI-3”} ,… ]

***


##分支容器(for VISSLM) （new in v1.1）
----------
项目中的配置项资源, 可列出配置项在三库

URI

		http://<server>/alm/rest/cm/project/{proId}/library/{type}/ci/{ciId}/?UToken={utoken}

方法:GET
***
返回值

		[ {type:"branch”, “name":"branchname","resource":"\<CM-URI\>"} ,… ]
		Or 
		[ {type:"root”, “name":"root","resource":"\<CM-URI\>"} ] 

***

##配置库路径资源(VISSLM)
----------
 \<CM-URI\> 配置库中的目录，文件资源，可获取，目录信息，文件数据，历史纪录   

URI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

		http://<server>/alm/rest/cm/project/{pid}/library/{type}/ci/{ciId}/{branch}/{*path}?UToken={utoken}


**方法:GET**

|参数 | 说明 |
| --- | :-- |
| return=summary (默认) | 缺省值，返回基本信息 |


返回值 

	{ type:”dir”, name:”folder1”, version:” 2223”, 
		member: [ 
			{"type":"file", "name":"任务书", "resource":"\<CM-URI\>", 
			  version:"1033", length;"2223", lmt:"2016-5-6", author:"user", “exprops”:{“规模”:”30”,…}} ,… 
			] } 
	Or 
	{type:”file”,name:”abc.c”, ,version:"1033",length;"2223",lmt:"2016-5-6",author:"user"}

***

|参数 | 说明 |
| :-- | :-- |
|return=data (可选) | 返回资源数据，目录则回所有的子数据，数据量过大时许使用zip参数|


返回值 

 		{ type:”dir”, name:”folder1”, member: [ {type:"file", "name":"任务书", "resource":"\<CM-URI\>", version:"1033", length;"2223", lmt:"2016-5-6", author:"user",data:”\<base64\>”}, {type:”dir”,name:”folder11”, resource:”\<CM-URI\>”, member:[…]} ,… ] } 
		Or 
		{type:”file”, name:”abc.c”, version:"1033", length;"2223", lmt:"2016-5-6", author:"user", data:”\<base64\>” } 
***

|参数 | 说明 |
| :-- | :-- |
| return=file (可选)| 返回资源文件，目录则返回所有的子文件的压缩文件(v0.4) |


返回值  文件流                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
***

|参数 | 说明 |
| :-- | :-- |                              
| version=\<ver\> (可选) pversion=\<pver\>| 指定返回对应版本的资源,不指定则默认取最新版本资源 Return=summary,data,file时有效 pversion仅针对产品库 |


返回值                                                                                           

		{ type:”dir”, name:”folder1”, 
			member: [ {type:"file", "name":"任务书", "resource":"\<CM-URI\>", version:"101", length;"2223", lmt:"2016-5-6", author:"user",data:”\<base64\>”},
		 ,… ] }
		or
 		{type:”file”, name:”abc.c”, version:"101", length;"2223", lmt:"2016-5-6", author:"user", data:”\<base64\>” } 

***
|参数 | 说明 |
| :-- | :-- |
| zip=true (可选)| return=data时，将返回数据压缩 return=file时, 返回压缩文件(目录无视开关,都是压缩文件) v1.7新增|


返回值

	{ type:”dir”, name:”folder1”, zip:”\<base64\>”} 
	Or
	{type:”file”, name:”abc.c”, version:"1033", length;"2223", lmt:"2016-5-6", author:"user", zip:”\<base64\>” }                                                                           

***

|参数 | 说明 |
| :-- | :-- |
| return=log (可选)| 返回历史纪录，默认取最新的100条 pversion 仅针对产品库有效,返回产品版本,version仅指配置项版本|
| start (可选)| 起始记录版本号，默认-1，表示最新版本 仅单return=log时有效， (v1.6)新增功能|
| end (可选)|结束记录版本号，默认0，表示初始版本；start〉end时表示从大的版本往回取，反之表示从小的版本记录往后取； 仅单return=log时有效 (v1.6)新增功能 |
| limit (可选) |返回最大纪录数，默认为50，表示最多返回50条历史记录 仅单return=log时有效 (v1.6)新增功能|


返回值      
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
	[ { "type":"log", version:"1003",pversion:"1.0", date:"2016-5-6 7:30", author:"user",message:"message", actions:[…] }， ]

 *** 

|参数 | 说明 |
| :-- | :-- |
| return=show (可选)  | 返回本身的显示信息(v0.8)

返回值                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              

	{ 
		"short":"任务书/任务书.docx", 
		"full": "[开发库][trunk]任务书/任务书.docx", 
		"ci-id": "133", 
		“ci-name”: ”任务书”, 
		"library-type":"开发库", 
		“branch”: ”trunk”, 
		“root-path”:” [开发库][trunk]任务书”, 
		“relative-path”:” /任务书.docx” }，   
                                                                                                                                                                                                                                                                                                                                                                                          
 *** 
                                                                                             
|参数 | 说明 |
| :-- | :-- |
| returnauth=true (可选) | 仅单return=summary时有效，将返回版本库的用户名密码加密信息（auth）                                                                        |

返回值

	{ type:”dir”, name:”folder1”,auth:”\<base64\>”} 
	Or 
	{type:”file”, name:”abc.c”, version:"1033", length;"2223", lmt:"2016-5-6", author:"user", auth:”\<base64\>” }

***
                                                                                             
|参数 | 说明 |
| :-- | :-- |
| returnactions=true (可选) | 仅单return=log时有效，将返回版本库每条日志的actions的信息 |


返回值

	{ type:”dir”, name:”folder1”,actions:”actions”} 
	Or 
	{type:”file”, name:”abc.c”, version:"1033", length;"2223", lmt:"2016-5-6", author:"user", actions:” actions” }
                                                                                                                                                                                                                                                                                                                                                                                                                                                                
***

**方法:POST 新建, 仅用于目录资源**

提交JSON字符串 ContentType=”application/json” 

如果使用Form方式，ContentType=”application/x-www-form-urlencoded”,同时把JSON字符串放在 param字段中 Request[“param”] 

userversion 参数仅用于VISSLM 

url 上传文件的地址，适配器主动获取 1.4版本增加; 1.9版本支持url作为一个目录，获取的文件流返回头部如果包含"visslmfiletype"并且值为"zipdir"时， 那么代表返回的数据流文件是一个目录的压缩文件，name为目录的名字，目录的内容就是压缩包里的文件内容。

	新建目录 {"type":"dir","name":"folder","message":"message…"，"user_version":"A"}  
	新建文件 {"type":"file","name":"file",data:"base64","message":"message…"，"user_version":"A"} 
	 Or 
	 {"type":"files", ,urls:[ {"name":"file","url":"url"}],"message":"message…"，"user_version":"A"}
	 Or {"type":"file","name":"file",url:"url","message":"message…"，"user_version":"A", result_code: "0",result_message: ""} 
	压缩包方式, 可以有文件和目录, 不包含当前目录 
	{ type:”zip”, zip:”\<base64\>”, "message":"message…"} or{ type:”zip”, url:”url”, "message":"message…"} 

返回值
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
	返回新建信息, 0.9 版本增加返回版本信息
	{"type":"dir","name":"source","resource":"\<URI\>","version":"12", "result_code": "0","result_message": "" } 
	or 
	{ "type":"file","name":"file","resource":"\<URI\>",length;"2223",lmt:"2016-5-6",author:"user","version":"12", "result_code": "0","result_message": "" } 
	Or 
	{"type":"more","resource":"\<DIFF_URI\>","version":"12"} 
	新建zip多条时的返回,返回的DIFF_URI能取到提交的细节内容(增删改)。  
	1.8 版本增加返回码
	result_code 返回码，正常可以不用返回，默认值0；如果有特殊情况，比如SVN的内容一样不能入库，那么返回一个”100”表示没有变化
	result_message 返回描述，正常可以不用返回，默认值空

                                                                         	
**方法:PUT 更新资源自身**

提交数据 JSON字符串，同POST方法 如果指定了name,并且与资源现有名字不同,那么使用新的名字重命名资源

	更新目录 {"type":"dir",zip:”\<base64\>” ,"message":"message…"，"user_version":"A", result_code: "0",result_message: ""} 
	Or 
	{"type":"dir","name":"source", url:"url" ,"message":"message…"，"user_version":"A", result_code: "0",result_message: ""}  
	更新文件 {"type":"file",data:"base64","message":"message…"，"user_version":"A", result_code: "0",result_message: ""} 
	Or 
	{"type":"file","name":"file",url:"url","message":"message…"，"user_version":"A", result_code: "0",result_message: ""}

返回值

	返回新建信息, 0.9 版本增加返回信息 {"version":"12"}
	1.8 版本增加返回码
	result_code 返回码，正常可以不用返回，默认值0；如果有特殊情况，比如SVN的内容一样不能入库，那么返回一个”100”表示没有变化
	result_message 返回描述，正常可以不用返回，默认值空

**方法:DELETE 删除 1.2版本修改** 

直接删除URL对应资源   

                                                                                             
|参数 | 说明 |
| :-- | :-- |
| message   | 删除操作的行为记录  |
| delself | true/false, 是否删除目录本身,默认为true,仅target为文件夹有效(1.3版本修改) |

	删除目录 {"type":"dir","name":"source","message":"message…"，"user_version":"A"} 
	删除文件 {"type":"file","name":"file","message":"message…"，"user_version":"A"}

返回值

	返回新建信息 {"version":"12"} 失败返回500

***

##版本库路径资源*(Adapter)*
----------
配置库中的目录，文件资源，可获取，目录信息，文件数据，历史纪录 svn用户名密码从URL中的user:password获取

方法及其他参数与VISSLM 方式一致
  
URI

	http://<server>/<cmadapter>/resouce 

                                                                                             
|参数 | 说明 |
| :-- | :-- |
| target=\<Path\>| 版本库中资源的真实路径，必添 |
| root=\<Path\>| 资源的根路径，主要用于某些版本管理工具识别配置项的根目录(2.0版本新增) |
| ver=\<svn ver\> | 版本库中要获取资源的版本(资源唯一)，选添，默认为-1(最新版) |
| auth=\<auth\> | 版本库所需的用户名密码加密信息 |
| depth=\<list_depth\>| 获取子目录的层级，默认为1，-1表示取所有层级的目录树，与return=summary/data配合使用。1.0增加此功能 |                                                                                                                     

**方法:POST 新建**

                                                                                             
|参数 | 说明 |
| :-- | :-- |                                               
| replace-all = true  | 对于目录资源如果设置了这个参数，那么将替换目录下所有原内容为最新内容(添加新的,更新已有的,删除没有的)，具体参考Webservice中的参数说明，默认参数为false |


返回值   
                                                                                                                                                     
	与VISSLM 方式一致 返回的资源<URI>的格式为 http://<server>/cmadapter/resouce?target=<subpath> 

***

##资源移库*(Adapter) v0.6*
----------
将给定的源URL中的所有内容,复制到目标URL中，支持多组 源库svn用户名密码从URL中的user:password获取  

URI 
	
	http://\<server\>/\<cmadapter\>/transmit       

**方法:POST**

                                                                                             
|参数 | 说明 |
| :-- | :-- | 
| replace-all = true  | 替换所有,如果为true,那么源路径下的内容将替换目标路径下所有内容(添加新的,更新已有的,删除没有的) 默认参数为true |


提交数据 JSON字符串，格式同其他资源里的POST方法 

	{ action_list: 
		[ {"type":"action", "source_url":"PATH", “source_version”:”1”, “target_url”:”PATH”, }, … ], 
		"message”:"MESSAGE",//移到外面 target_user:”\*”, //目标用户名如果为\*表示与源用户名密码一致 
		target_password:""
	} 

返回值  
                                                                                                                                                                                                                                                                                                                           
	返回版本, 0.9 版本增加返回信息 {"version":"12", result_code: "0",result_message: "",versioninfo:[{"TargetVersion":"1","TargetURL":"","SourceURL":"","SourceRevision":"1"}...]} Or HttpException,状态码 500
 	1.8 版本增加返回码
	result_code 返回码，正常可以不用返回，默认值0；如果有特殊情况，比如SVN的内容一样不能入库，那么返回一个”100”表示没有变化
	result_message 返回描述，正常可以不用返回，默认值空
	2.1 新加多个目标的版本信息   
	versioninfo 版本信息，多个目标返回每个目标的版本信息
		TargetVersion 目标的最新库的版本号
		TargetURL 目标路径
		SourceURL 源路径
		SourceRevision 源库的版本号

***

##资源打包*(Adapter) v0.6*
----------
每个源在目标URL位置创建一个名为\< SubFolder\>的子目录, 各个源URL中的所有内容,复制到目标URL对应的子目录中 源库svn用户名密码从URL中的user:password获取       

URI                                                                                                                                                                                                                                                                                                                           

	http://<server>/<cmadapter>/package

**方法:POST**
                                                                                                                                                                                                                                                                                                                         
                                                                                             
|参数 | 说明 |
| :-- | :-- |
| replace-all = true  | 替换所有,如果为true,那么源路径下的内容将替换目标路径下所有内容(添加新的,更新已有的,删除没有的) 默认参数为true |

提交数据 JSON字符串，格式同其他资源里的POST方法 

	{ 
		source_list: [ 
			{"type":"source","source_url":"PATH",“source_version”:”1”, “sub_folder”:”FOLDERNAME” },
			{"type":"source","source_url":"PATH",“source_version”:”2”, “sub_folder”:”FOLDERNAME” }, … ],
			target_url:”PATH”, “message”:”MESSAGE”, target_user:”\*”, //目标用户名如果为\*表示与源用户名密码一致
		target_password:""
	} 


返回值                                                                                                                                                                                                                                                                                                                                                                                                                                     

	返回版本, 0.9 版本增加返回信息 {"version":"12"} Or HttpException,状态码 500

***

##适配器版本说明
----------
获取适配器的版本说明
URI
	
	http://<server>/cmadapter/api/about
                                                                                      
                                                                           
**方法:GET** 

返回值

		返回版本信息串 { name:\<适配器名称\>, version:\<版本\>, description:\<描述\> } Or HttpException,状态码 500

***

##委托UI


###选择一个目录或者文件以及版本 
----------

对于VISSLM来说界面中需要选择项目与配置库类型,然后才是目标资源版本 

对于Adapter来说界面中需要指定起始路径,接着选择目标资源（目录或文件）与版本

URI

		http://<server>/alm/rest/cm/ui/selecturlversion   （visslm）
		http://<server>/cmadapter/ui/selecturlversion  （adapter）


                                                                                             
|参数 | 说明 |
| :-- | :-- |
| pid=xxx (for visslm)  | 默认的项目 |
| librarytype = dynamic (for visslm)  | 默认的库类型                                                                                                       |
| change_project=false (for visslm)                                                                                                                                         | 界面中不可切换项目，必须指定pid参数                                                                                |
| change_librarytype=false (for visslm)                                                                                                                                     | 界面中不可切换库类型，必须指定librarytype参数                                                                      |
| root=&lt;path&gt; (for adapter)                                                                                                                                               | 默认起始路径                                                                                                       |
| target=&lt;CM-URI&gt;                                                                                                                                                         | 默认选择的资源，仅仅是版本库URL；当resource参数不为空时无效                                                        |
| auth=&lt;auth&gt;                                                                                                                                                             | 版本库所需的用户名密码加密信息，仅target参数有效时有效                                                             |
| resource=&lt;URL&gt;                                                                                                                                                          | 默认选择的资源，URL中带有target和auth参数，如果有resource参数且不为空，则target=&lt;CM-URI&gt;参数无效                 |
| version=&lt;ver&gt;                                                                                                                                                           | 默认搜索的最大版本号                                                                                               |
| defaultVersion=&lt;ver&gt; | 默认选中的版本号 |
| targetType=[dir&brvbar;file&brvbar;all] | 选择目标资源类型,默认为all |
| fileSuffix="rar,zip" | 资源后缀限定，默认为不限定，当targetType为dir时无效|

返回

		{ type: “OK”, data：{"verion":"v1.0","resource":"\<URL\>"} } 
		Or 
		{ type: “CANCEL” } 

***

###选择一个资源的历史版本 根据指定资源，显示其历史版本与记录，从其中选择一个版本号返回                                                                                       
----------
URI                                                                                                                                                                       
	
	http://<server>/alm/rest/cm/ui/selectversion   （visslm）
	http://<server>/cmadapter/ui/selectversion  （adapter）


                                                                                             
|参数 | 说明 |
| :-- | :-- |
| target=\<CM-URI\>                                                                                                                                                         | 默认选择的资源，仅仅是版本库URL；当resource参数不为空时无效                                                        |
| auth=\<auth\>                                                                                                                                                             | 版本库所需的用户名密码加密信息，仅target参数有效时有效，可为空                                                     |
| resource=\<URL\>                                                                                                                                                          | 默认选择的资源，URL中带有target、auth、和return=log子参数，如果有resource参数且不为空，则target=\<CM-URI\>参数无效 |
| version=\<ver\>                                                                                                                                                           | 默认搜索的最大版本号                                                                                               |
| defaultVersion=\<ver\>                                                                                                                                                    | 默认选中的版本号                                                                                                   


返回                                                                                                                                                                      

	{ type: “OK”, data：{"verion":"v1.0"} }

***

##错误处理
----------
返回HttpException

如果是资源不存在，一般返回404

如果是参数格式不正确，一般返回400

如果是服务器执行错误，一般返回500


#附录
----------

示例代码

发送请求
	
	String urltest = "http://192.168.1.133/alm/rest/cm/ci/333";
	
	Uri uri = new Uri(urltest);
	
	HttpWebRequest request = (HttpWebRequest)WebRequest.Create(uri);
	
	request.Method = "POST";
	
	//request.ContentType = "application/json;charset=UTF-8";
	
	string authInfo = Convert.ToBase64String(Encoding.Default.GetBytes("Junius:1"));
	
	request.Headers["Authorization"] = "Basic " + authInfo;
	
	string inputData = "{\\"aaa\\":\\"helloworld!\\"}";
	
	string postFormData = "param=" + inputData;
	
	string postData = "{\\"aaa\\":\\"helloworld!\\"}";
	
	UTF8Encoding encoding = new UTF8Encoding();
	
	byte[] byte1 = encoding.GetBytes(postFormData);
	
	// Set the content type of the data being posted.
	
	request.ContentType = "application/x-www-form-urlencoded";
	
	//request.ContentType = "application/json";
	
	// Set the content length of the string being posted.
	
	request.ContentLength = byte1.Length;
	
	Stream newStream = request.GetRequestStream();
	
	newStream.Write(byte1, 0, byte1.Length);
	
	// Close the Stream object.
	
	newStream.Close();
	
	try
	
	{
	
	HttpWebResponse response = (HttpWebResponse)request.GetResponse();
	
	//Stream myResponseStream = response.GetResponseStream();
	
	//StreamReader myStreamReader = new StreamReader(myResponseStream,
	Encoding.GetEncoding(encoding));
	
	//retString = myStreamReader.ReadToEnd();
	
	//myStreamReader.Close();
	
	//myResponseStream.Close();
	
	}
	
	catch (WebException ex)
	
	{
	
	byte[] contentBytes = new byte[ex.Response.ContentLength];
	
	ex.Response.GetResponseStream().Read(contentBytes,0,(int)ex.Response.ContentLength);
	
	string content = encoding.GetString(contentBytes);
	
	}

处理请求

	string contentType = request.ContentType;
	
	int idx = contentType.IndexOf(";");
	
	contentType = (idx == -1) ? contentType : contentType.Substring(0, idx);
	
	string content;
	
	if (contentType == "application/x-www-form-urlencoded")
	
	{
	
	content = request.Form["param"];
	
	}
	
	else
	
	{
	
	byte[] contentBytes = new byte[request.ContentLength];
	
	request.InputStream.Read(contentBytes, 0, request.ContentLength);
	
	content = request.ContentEncoding.GetString(contentBytes);
	
	}
	
	List\<Dictionary\<string, string\>\> pData = null;
	
	try
	
	{
	
	pData = JsonConvert.DeserializeObject\<List\<Dictionary\<string,
	string\>\>\>(content);
	
	}
	
	catch (System.Exception ex)
	
	{
	
	throw new HttpException(400, ex.Message);
	
	}


##ChangeLog

|版本 |更新 |
| :-- |:--| 
|v1.9|上传入库行为（Post/Put）增加对目录url的支持|
|v1.8|入库行为（Post/Put/移库）增加两个返回值result_code，result_message，处理无变化入库失败问题|