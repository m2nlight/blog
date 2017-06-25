# MySQL Entity EF6 配置 ADO.NET 实体数据模型

步骤：

1) 在您的项目下创建lib文件夹，然后拷贝packages中的EntityFramework.6.1.3、MySql.Data.6.9.9和MySql.Data.Entity.6.9.9到lib下

2) 在您的项目下，引用这些lib中对应的dll，分别是EntityFramework.dll、MySql.Data.dll和MySql.Data.Entity.EF6.dll

3) 在您的项目中添加应用程序配置文件App.config，编辑App.config，内容如下

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
  </configSections>
  <entityFramework>
    <providers>
      <provider invariantName="MySql.Data.MySqlClient" type="MySql.Data.MySqlClient.MySqlProviderServices, MySql.Data.Entity.EF6, Version=6.9.9.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d"></provider>
    </providers>
  </entityFramework>
  <system.data>
    <DbProviderFactories>
      <remove invariant="MySql.Data.MySqlClient" />
      <add name="MySQL Data Provider" invariant="MySql.Data.MySqlClient" description=".Net Framework Data Provider for MySQL" type="MySql.Data.MySqlClient.MySqlClientFactory, MySql.Data, Version=6.9.9.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d" />
    </DbProviderFactories>
  </system.data>
</configuration>
```

4) 在您的项目中新建一个DataModel文件夹，用来保存数据模型，然后右键DataModel -> 添加 -> 新建项，选择 Visual C#/数据/ADO.NET 实体数据模型，输入文件名如：MyDataModel，添加后会启动一个配置向导。

5) 选择“来自数据库的 EF 设计器”下一步，配置连接，在连接的高级设置里配置Charset=utf8，数据库版本要求MySQL5.6，选择“是，在连接字符串中包括敏感数据”，将 App.Config 中的连接另存为如“dbnameEntities”，下一步，会自动选择EF6并进入对象选择界面，选择需要的表，完成。


