邮件RestApi说明

----------

#发送指定邮件内容的邮件
##场景说明：
	发送指定邮件内容的邮件
##接口地址：
	url：http://<server>/alm/rest/api/SendSPMail
	请求方式：Post
##参数输入：
	parameter（string），必填，邮件基本信息Json字符串，Key值说明如下：
		SendTo（string），收件人地址，多个地址逗号分隔；
		SendCc（string），抄送人地址，多个地址逗号分隔；
		SendBcc（string），密送人地址，多个地址逗号分隔；
		Subject（string），邮件标题；
		Body（string），邮件正文。
##结果输出：
	对象，具体Key，Value说明如下：
	ErrorCode：0（成功）/-1（失败）
	ErrorMsg：成功(0)/失败(-1)
	Data：bool（true/false）
