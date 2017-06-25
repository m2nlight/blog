# 配置App.config、App.Debug.config和App.Release.config

**1. 卸载项目**

**2. 编辑 csproj 文件，添加下面4块内容**

(1) 在最后一个PropertyGroup下面添加：

```
<PropertyGroup>
  <ProjectConfigFileName>App.config</ProjectConfigFileName>
</PropertyGroup>
```

(2) 在最后一个ItemGroup下面添加：

```
<ItemGroup>
  <None Include="App.config" />
  <None Include="App.Debug.config">
    <DependentUpon>App.config</DependentUpon>
  </None>
  <None Include="App.Release.config">
    <DependentUpon>App.config</DependentUpon>
  </None>
</ItemGroup>
```

(3) 在最后一个Import下面添加：

```
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\Web\Microsoft.Web.Publishing.targets" />
```

（注：因为VS2015的目录位置是：C:\Program Files (x86)\MSBuild\Microsoft\VisualStudio\v14.0\Web\Microsoft.Web.Publishing）

(4) 在最后添加：

```
<Target Name="AfterBuild">
  <TransformXml Source="@(AppConfigWithTargetPath)" Transform="$(ProjectConfigTransformFileName)" Destination="@(AppConfigWithTargetPath->'$(OutDir)%(TargetPath)')" />
</Target>
```

**3. 重新载入项目**

**4. App.config、App.Debug.config和App.Release.config可能为叹号，可分别创建如下：**

(1) App.config

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
  </appSettings>
</configuration>
```

(2) App.Debug.config

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <appSettings>
    <add key="Mode" value="Debug" xdt:Transform="Insert"/>
  </appSettings>
</configuration>
```

(3) App.Release.config

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <appSettings>
    <add key="Mode" value="Release" xdt:Transform="Insert"/>
  </appSettings>
</configuration>
```

**5. 分别用Debug和Release模式编译项目，就能看见插入的appSettings/Mode了。**

