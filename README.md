# j2Cache-sdk
j2Cache 二次开发
修改点一: 修改Spirngboot 2.6版本集成j2Cache 配置在nacos读取不到的问题

![image](https://github.com/xiejie2438/j2Cache-sdk/assets/38717856/ea8b25d9-d428-4ec5-9287-c7a792be3f29)
是CompositePropertySource对象才往下走，我们debug一下发现对应的示例是BootstrapPropertySource
![image](https://github.com/xiejie2438/j2Cache-sdk/assets/38717856/42cafb08-70c4-4302-a148-29595f0d4dbe)

继续查看nacos的源码，如下这边发现是是CompositePropertySource,那这样的话nacos集成这块是没问题的
![image](https://github.com/xiejie2438/j2Cache-sdk/assets/38717856/ce3b87bd-6bd2-4bae-8ce4-1e7ead62e985)
在往下看下Springboot 程序加载，发现这变获取到的propertySource全都new BootstrapPropertySource()，发现原因，改造j2cache源码修改initFromConfig方法
![image](https://github.com/xiejie2438/j2Cache-sdk/assets/38717856/6c0c134e-0ffe-4c2f-8bce-fe1eda3937df)

![image](https://github.com/xiejie2438/j2Cache-sdk/assets/38717856/21af1bd8-6817-44b8-840b-e55ec1f0218c)

修改点二：缓存lettuce配置会影响整个项目的redis配置

