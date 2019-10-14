IIS配置HTTPS说明

 1. IIS管理器导入证书

   ![](image\https\server.JPG)

 2. 导入证书

  ![](image\https\importkey.JPG)

 3. 绑定协议

  ![](image\https\binding.JPG)

 4. https自行测试相关资料

  * 测试证书下载(正式证书由客户提供): [visslm.com](image    \https\visslm.com.zip)
  * 证书测试域名为visslm.com
  * 按照1-3步配置https证书
  * 在服务器及客户机C:\Windows\System32\drivers\etc\hosts   增加
     127.0.0.1 visslm.com    *127.0.0.1修改为服务器IP*
   
  * 在服务器及客户机安装测试CA证书visslmCA.cer,安装说明
 
   ![](image\https\installkey1.JPG)
  
   ![](image\https\installkey2.JPG)
 