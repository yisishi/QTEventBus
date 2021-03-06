## 基础使用

### 替代AppDelegate

用QTAppDelegate替代默认的AppDelegate，修改main.m:

```
return UIApplicationMain(argc, argv, nil, NSStringFromClass([QTAppDelegate class]));
```

> 也可以继承QTAppDelegate，但是记得要在方法里调用super。

## 注册模块

用宏QTAppModuleRegister来注册模块，其中注册的类需要实现协议`QTAppModule`

```
// 两个参数分别是类名和优先级
QTAppModuleRegister(PayService, QTAppEventPriorityDefault)
```

## 响应事件

实现协议`QTAppModule`种的方法

```
@interface PayService()<QTAppModule>
@end
@implementation PayService

/// 每一次事件来的时候，EventBus调用这个方法来生成实例
+ (id<QTAppModule>)moduleInstance{
    return [[PayService alloc] init];
}

/// App启动
- (void)appDidFinishLuanch:(QTAppDidLaunchEvent *)event{
    NSLog(@"PayService: appDidFinishLuanch");
}

@end

```

