---
layout: post
title: My Jekyll Theme
comments: true
category: portfolio
tags:
    - web-development
    - jekyll
    - theme
---  

##UITabBarController用法
**官方解释：**  

  * 通过赋予UITabBarController的属性viewControllers，来配置每个tab切换所对应的controller。viewControllers中每个元素的顺序决定了在页面中哪个tab对应的view会默认显示，如果要手动指定一个要显示的view，通过指定属性selectedViewController来设置默认指定的view。或者使用selectedIndex也可以来指定要默认显示的view。
  * 每个tabbar的tabbar item是根据它自身对应的controller来进行配置的。如果要让tabbar item和其相关的controller进行关联，那么就要创建一个UITabBarItem实例，然后指定给响应的controller。例如：  
  `firstViewController.tabBarItem = [[UITabBarItem alloc] init];`  若没有指定特定的tabBarItem，那么当前页面对应的viewcontroller会创建一个默认的没有图片的item且item的title为viewcontroller的title内容。
  * UITabBarControllerDelegate protocol.任何一个tab切换都会触发与delegate发送消息。通过delegate可以完成特定tabbar 被选中的时候执行额外的方法。这些delegate方法都是可选的。  
  
  ```
  //用于决定当前选中的viewController是否响应,返回NO，则当前的viewcontroller一直保持active状态，别的viewcontroller无法点击响应。
- (BOOL)tabBarController:(UITabBarController *)tabBarController
shouldSelectViewController:(UIViewController *)viewController  
//确定用户当前点击的是哪个tab对应的viewcontroller
- (void)tabBarController:(UITabBarController *)tabBarController 
didSelectViewController:(UIViewController *)viewController
  
  ```
  **UITabBar**  
  1.`@property(nonatomic) UIBarStyle barStyle`tabbar的样式描述
  现在只有两种还在用：UIBarStyleDefault,UIBarStyleBlack.  
  2.`@property(nonatomic, retain) UIColor *barTintColor`  设置tabbar的背景颜色。这个颜色默认会有透明效果，若要不显示透明效果，设置tabbar的translucent属性为NO。 
  3.`@property(nonatomic, retain) UIColor *tintColor`设置点击变色后的title颜色。  
  4.`@property(nonatomic, retian) UIImage *backgroundImage`设置tabbar的背景图片，会将图片进行拉伸填充
  
  **UITabBarItem：**UITabBarItem是UITabBar的一个item元素。使用`initWithTabBarSystemItem:tag:`方法来使用一个系统的item，使用`initWithTitle:image:`方法来吊用一个自定义的item，但是这时image的选中状态和非选中状态都是同一个，若要让选中图案和非选中图案不一样那么使用`initWithTitle:image:selectedImage:`来创建一个自定义的item。  
  
  ```
  //使用系统提供的一个item样式，title和image不能改变
  - (instancetype)initWithTabBarSystemItem:(UITabBarSystemItem)systemItem tag:(NSInteger)tag
  ```
  UITabBarSystemItem
  >typedef enum {  
  >  UITabBarSystemItemMore,  
  UITabBarSystemItemFavorites,   
   UITabBarSystemItemFeatured,   
   UITabBarSystemItemTopRated,   
    UITabBarSystemItemRecents,  
    UITabBarSystemItemContacts,  
    UITabBarSystemItemHistory,  
   UITabBarSystemItemBookmarks,  
   UITabBarSystemItemSearch,  
   UITabBarSystemItemDownloads,  
    UITabBarSystemItemMostRecent,  
    UITabBarSystemItemMostViewed,  
    }UITabBarSystemItem  
    
```
//自定义一个图片和标题的item，这里未选中和选中同时使用这个图片
-(instancetype)initWithTitle:(NSString *)title image:(UIImage *)image tag:(NSInteger)tag
```

```
//自定义图片和标题，设置图片的选中和非选中不同图片
- (instancetype)initWithTitle:(NSString *)title image:(UIImage *)image selectedImage:(UIImage *)selectedImage;
```
属性描述:  
1.`@property(nonatomic, copy) NSString *badgeValue`用于标注右上角的小红点消息按钮。  
2.`@property(nonatomic, retain) UIImage *selectedImage`默认的时候会设置从源图片进行alpha处理后的效果图，如果要保留原来图片的样式不变，那么要设置图片的UIImageRenderingModelAlwaysOrignal属性。

![Demo 图片截图](http://7xleoh.com1.z0.glb.clouddn.com/tabbarDemo.png)

[git Demo地址](https://github.com/Shawn-WangDapeng/UITabBarControllerDemo.git)

