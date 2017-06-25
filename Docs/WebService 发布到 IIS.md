# WebService 发布到 IIS

### 安装IIS，注册.NET Framework 4.0 ASP.NET服务

1) 安装IIS。打开Windows程序和功能，启用或关闭Windows功能，勾选IIS服务（Internet Information Services），确定。

2) 注册ASP.NET。用管理员身份打开CMD，输入：

```
C:\> cd C:\Windows\Microsoft.NET\Framework\v4.0.30319
C:\> aspnet_regiis.exe -i
```

3) 配置IIS。打开Internet信息服务(IIS)管理器（inetmgr.exe），选择“应用程序池”，右侧会看见ASP.NET v4.0和ASP.NET v4.0 Classic，如果没有，需要手动右键右侧列表，添加应用程序池，选择.NET 4.0版本。

4) 创建Web应用发布文件夹，假设在`C:\inetpub\MyWebService`(如果将指定某个账户运行，需要在安全里添加)。**设置这个文件夹共享**，用于后面VS发布用。

5) 添加应用程序。右键默认网站，添加应用程序，别名输入假设`MyWebService`，应用程序池选择`ASP.NET v4.0`，物理路径浏览到`C:\inetpub\MyWebService`，点“连接为”，指定一个账户（比如管理员账户和密码），点“测试设置”，没有问题点“确定”。

6) 其他配置。目录浏览：选择新建立的应用节点，双击“目录浏览”，右侧改为启用。默认文档：双击默认文档，删除不需要的默认文件。


### VS2015发布WebService

1) 在VS里右键要发布的Web应用，点“发布”
2) 点“自定义”，输入任意名称，假设`MyWebService`
3) 发布方法（Publish method）选择文件系统（File System），目标位置输入：`\\xxxxxxx\MyWebService`，其他默认。
4) 最后一步点“发布”按钮。


### 浏览

输入：`http://xxxxxxx/MyWebService/xxxxxxx.asmx` 或者 aspx

