---
layout:     post
title:      深度学习
subtitle:   人工智能
date:       2020-12-26
author:     GuiZhaoyang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - AI
    - 深度学习
    - CV
    - 开源框架
---

# Rea础


# ReactiveCocoa开发中常见用法

1. 替换代理			
2. 替换KVO
3. 监听事件
4. 替换通知
5. 监听文本框文字改变
6. 统一处理多个网络请求



#### 替换代理：

**rac_signalForSelector:**

`rac_signalForSelector:` 直接监听 `Selector` 事件的调用

应用场景：监听 `RedViewController` 中按钮的点击事件 `btnTap:`

跳转到`RedViewController`前，先使用`rac_signalForSelector`订阅rvc中的 `btnTap:` 点击事件

```
// 使用segue跳转
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
- 
    if ([segue.identifier isEqualToString:@"goRedVC"]) {
        
        RedViewController *rvc = segue.destinationViewController;
        
        // 订阅rvc中的 btnTap: 点击事件
        [[rvc rac_signalForSelector:@selector(btnTap:)] subscribeNext:^(id x) {
        
            NSLog(@"RedVC btnTap！");
        }];
    }
}
```

`RedViewController.m` 中的按钮事件

```
- (IBAction)btnTap:(id)sender {
    
    NSLog(@"!");
}
```

#### 替换KVO

**rac_valuesForKeyPath:**

```
// KVO
// 监听 slider 的 value 变化
[[self.slider rac_valuesForKeyPath:@"value" observer:nil] subscribeNext:^(id x) {

    NSLog(@"slider value Change：%@", x);
}];
```

#### 替换通知

**rac_addObserverForName**

```
// 原生的订阅通知
[[NSNotificationCenter defaultCenter] addObserver:self
                                         selector:@selector(userDidChange:)
                                             name:kTTCurrentUserLoggedOffNotification
                                           object:nil];
                                           
// 使用RAC订阅通知 ，takeUntil限定信号的声明周期                                  
[[[[NSNotificationCenter defaultCenter] rac_addObserverForName:UIApplicationDidEnterBackgroundNotification object:nil]
  takeUntil:[self rac_willDeallocSignal]]
  subscribeNext:^(id x) {
     NSLog(@"Notification received");
}];
```

#### 监听事件

**rac_signalForControlEvents:**

```
// 监听 btn 的 UIControlEventTouchUpInside 点击事件
[[self.btn rac_signalForControlEvents:UIControlEventTouchUpInside] subscribeNext:^(id x) {
    
    NSLog(@"btnTap");
}];
```


#### 监听 textField 文字变化

**！

