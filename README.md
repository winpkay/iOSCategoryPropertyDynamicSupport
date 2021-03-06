# iOSCategoryPropertyDynamicSupport
iOS Class Category property dynamic support
 
 在运行时自动给分类的动态属性添加相应的 `getter`、`setter` 方法</br>  
 在分类中添加一些自定义的属性的场景还是蛮多的。一般的方法是自定义其 `getter`、`setter` 方法，在这些方法  
 里面再用关联对象等手段来实现。虽然不难，却也麻烦且重复。  
 本类的目的在于解放这些重复的劳动。  
 
 　使用：  
 　　1、导入本类及相关类（NSObject+nl_dynamicPropertySupport目录下）  
 　　2、在分类中定义属性时，默认要以 `nl_` 开头  
 　　3、在分类的实现体中，给属性加上 @dynamic  
 
 　优点：  
 　　1、所有的对象、基本数据类型  
 　　2、支持系统已有的 [NSValue valueWith...] 方法的结构体（详见 NSValue ）。如：CGRect  
 　　3、支持 KVC  
 　　4、支持 KVO  
 　　5、支持 strong、copy、weak  
 
 　不足：   
 　　1、不支持自定义的结构体。   
 　　　但可以通过 `+ nl_missMethodWithPropertyDescriptor:selector:` 来实现。实现方法可见：（`nl_dynamicPropertyCustomeStruct`分类）  
 　　2、注意：KVO 支持不完美。  
 　　　当观察动态生成的 weak 属性时，不会接收到 weak 自动设置为 nil 的通知（在 weak 指向的对象被销毁时，weak 属性会自动设置为 nil）。  
 
##工作原理：
 　　1、使用 `Associated Objects`  
 　　2、OC runtime  
 　　3、Type Encoding  
 　　详见：http://nathanli.cn/2015/12/14/objective-c-%E5%85%83%E7%BC%96%E7%A8%8B%E5%AE%9E%E8%B7%B5-%E5%88%86%E7%B1%BB%E5%8A%A8%E6%80%81%E5%B1%9E%E6%80%A7/  
 　　
##代码使用：
 头文件 .h：  
 ```Objective-C
 @interface YourClass (YourCategory)
 
 @property NSString *nl_yourProperty;
 
 @end
 ```
 
 实现文件：  
 ```Objective-C
 @implementation YourClass (YourCategory)
 
 @dynamic nl_yourProperty;
 
 @end
 ```
 
##自定义属性前辍  
  1、`#import "NLDynamicPropertyPrefix.h"` </br>
  2、 设置前辍 `DynamicPropertySetPrefix("demo_")` </br>
  注意，要在 m 文件中调用；前辍名长度不能为 0，你应该定义成字母加下划线的形式；不能重复调用。
  
 
 
  　如果你有好的 idea 或 疑问，请随时提 issue 或 request。 
 
##License
Released under the MIT-license
