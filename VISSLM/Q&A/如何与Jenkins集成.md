#VISSLM 与 Jenkins 集成

##从VISSLM触发Jenkins构建
-------

###Jenkins设置

1. 创建一个新用户

	Manage Jenkins->Manage Users->Create User

	输入用户名密码，然后点击注册，这里假设用户名为user

2. 在任务设置中激活Trigger builds remotely (e.g., from scripts)，这个token是自己设定的

	![](./VISSLM/Q&A/jenkins01.png)
　　

3. 给用户添加权限

	Manage Jenkins->Configure Global Security
	
	勾选Access Control下的matrix-based security，然后将test用户添加到列表里面
	
	只需要以下权限即可：
	
	 - Overall Read
	 - Job Build
	 - Job Read
	 - Job Workspace

4. 创建URL

	用user账号登录，从右上角点击用户，进入用户设置，点击Show API Token...
	
	![](./VISSLM/Q&A/jenkins02.png)


根据这些内容，就可以创建一个这样的URL：

　　http://user:bee0a00a72dce1263ef8d25d7d7d9a6@your-jenkins.com/job/JobName/build?token=80

***

###VISSLM设置

1. 新建一个类型
	
	![](./VISSLM/Q&A/jenkins03.png) 
  
2. 创建三个个字段

	Job

	![](./VISSLM/Q&A/jenkins04.png)  

	Token

	![](./VISSLM/Q&A/jenkins09.png)
 
 	BuildLog

	![](./VISSLM/Q&A/jenkins10.png)  

	部件

	![](./VISSLM/Q&A/jenkins11.png)  

3. 创建Jenkins服务

	![](./VISSLM/Q&A/jenkins05.png)  

4. 配置策略

	![](./VISSLM/Q&A/jenkins06.png)  

5. 项目中新建Job对象

	![](./VISSLM/Q&A/jenkins07.png)  

6. 执行策略

	![](./VISSLM/Q&A/jenkins08.png)  

	成功触发Jenkins构建

***

##Jenkins 回写数据到 VISSLM
---------

VISSLM 已开放开发接口

- WebService
- RestAPI

PYTHON 已经可以通过接口实现VISSLM数据操作

Jenkins支持运行Python脚本

因此Jenkins可通过Python与VISSLM集成

###Jenkins设置

添加参数

![](./VISSLM/Q&A/jenkins12.png) 
 
安装 Python 插件, 之后配置

![](./VISSLM/Q&A/jenkins13.png) 

重新从VISSLM 触发构建,构建完成后,VISSLM中已得到构建信息

![](./VISSLM/Q&A/jenkins14.png) 

**谢谢阅读**

