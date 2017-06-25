# CSharp 缓存

.NET Framework 4.0 加入了类似Web缓存的缓存框架。下面是简单使用缓存框架的方法：

1. 添加引用：System.Runtime.Caching
2. 插入缓存代码

```
public static string Foo(string bar)
{
  // 检查输入参数
  if(string.IsNullOrEmpty(bar))
  {
    return null;
  }

  // 从缓存中查找并返回
  var cacheKey = $"Foo+{bar}";  // 配置全局不重名的缓存key（我用加号分隔缓存名，保证唯一并且可以被遍历）
  var cache = MemoryCache.Default; // 使用内存缓存
  if (cache.Contains(cacheKey))  // 检查是否包含了缓存
  {
    var cacheResult = cache.Get(cacheKey) as string;  // 获取缓存数据
    return cacheResult;  // 返回缓存结果
  }

  // 未找到缓存数据，获取数据，然后加入缓存中，再返回
  var r = DoSomething(bar);  // 获得结果
  if(string.IsNullOrEmpty(r))  // 检查结果是否正确
  {
    return r; // 错误结果不加入缓存，直接缓存
  }
  var policy = new CacheItemPolicy // 创建缓存策略
  {
    AbsoluteExpiration = DateTimeOffset.Now.AddMilliseconds(10*60*1000); // 10分钟后删除的策略
  };
  cache.Set(cacheKey, r, policy); // 加入缓存
  return r; // 返回结果
}
```

手动清除缓存指定key的代码：

```
public static void ClearFooCache()
{
  var cacheKeyPrefix = "Foo+";
  var cache = MemoryCache.Default;
  var array = cache.Where(n => n.Key.StartsWith(cacheKeyPrefix)).Select(n => n.Key).ToArray();
  foreach (var key in array)
  {
    cache.Remove(key);
  }
}
```