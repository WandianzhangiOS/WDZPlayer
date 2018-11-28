# WDZPlayer
万店掌播放器



## 对象释义 (必传)
开放平台字段 | KDVideoModel  
---|---
mediaServerIp |  mediaServerIp
mediaServerPort | mediaServerPort
 puid |  puid
 channel_id |  channel_id
 video_id |  vsc 
 name |  name
 slaveChannel_id |  slaveChannel_id
 id |  ID
 ptzEnable |  ptzEnable
 audioCallEnable |  audioCallEnable
 online |  status
 
开放平台字段 | KDShopModel
---|---
id | ID
name | name

## 注意：使用SDK时需设置

1. 项目->Targets->Build Settings->compile sources As->Objective-C++
2. 将framwork拖到 项目->Targets->Build Phases ->copy Bundle Resources中或者将项目中的任意一个.m文件改成.mm

#### 1.依赖第三方

```
  pod 'AFNetworking'
  pod 'MJExtension'
  pod 'FMDB'
  pod 'RegexKitLite'
  pod 'SDWebImage'
```
#### 2.依赖框架

```
libicucore.tdb
libbz2.tbd
libz.tdb
libiconv.tbd
OpenGLES.framework
UIKit.framework
Foundation.framework
AudioToolbox.framework
Foundation.framework
QuartzCore.framework
CoreGraphice.framework
```

#### 3.Header文件介绍

- 0.注册类：WDZService

```
    //asid 开放平台获取
    //token 对接万店掌系统中用户的token
    + (void)registerWDZPlayerWithAsid:(NSString *)asid token:(NSString *)token;
```


- 1.摄像头对象 ==KDVideoModel==,使用字典创建video对象

```
    -(instancetype)initWithDictionary:(NSDictionary *)dic;
```

     
- 2.门店对象 ==KDShopModel==,使用字典创建ShopVideo对象
   
```
    -(void)parseModelWithDic:(NSDictionary *)dic;
```

     
- 3.视频界面播放控制器 ==KDMPlayViewController==
   
```
    //门店对象
    @property (strong , nonatomic) KDShopModel *shop; 
    //需要当前展示的摄像头
    @property (nonatomic, strong) KDVideoModel *currentShowModel; 
    //需要展示的摄像头的列表
    @property (nonatomic, strong) NSArray *videoList; 
```

- 4.播放器界面配置类 ==KDWDZConfig== 
    - 注意:在跳转KDMPlayViewController前设置
    
```
//点击抓拍图片的通知
#define kReceivePhotoNotification @"kReceivePhotoNotification"
//点击快拍按钮的通知
#define kQuickShotNotification  @"kQuickShotNotification"

//默认配置  主题色是橘黄色 导航栏 白色 导航栏 字体大小20 字体颜色 51
+ (instancetype)defaultConfig;

//主题色
@property (nonatomic, copy) UIColor *themeColor;

//导航栏  默认为白色
@property (nonatomic, copy) UIColor *navigationBarColor;

//导航栏 字体大小
@property (nonatomic, copy) UIFont *navigationTitleFont;

//导航栏 字颜色
@property (nonatomic, copy) UIColor *navigationBarTitleColor;

//回放时间轴背景颜色
@property (nonatomic, copy) UIColor *timeLineBackgroundColor;

//是否使用内部的图片浏览器，在抓拍图片处，查看图片 默认不启用，外部处理
@property (nonatomic, assign) BOOL isUseInternalPhotoBrowser;
```


#### 3.使用步骤

##### 3.1注册

```
//app启动时注册
[WDZService registerWDZPlayerWithAsid:<#your aid#> token:<#userToken#>];

```

###### 3.2使用

```
    KDMPlayViewController *vc = [[KDMPlayViewController alloc] init];
    vc.currentShowModel = self.video;
    vc.videoList = self.videoList;
    vc.shop = self.shopmodel;
    [self.navigationController pushViewController:vc animated:YES];
```





