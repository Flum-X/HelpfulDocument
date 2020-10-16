### 核心原则

**一、代码应该简洁易懂，逻辑清晰**

* 不要过分追求技巧，降低程序的可读性。
* 简洁的代码可以让bug无处藏身。要写出明显没有bug的代码，而不是没有明显bug的代码。

**二、面向变化编程，而不是面向需求编程**

需求是暂时的，只有变化才是永恒的。
本次迭代不能仅仅为了当前的需求，写出扩展性强，易修改的程序才是负责任的做法，对自己负责，对公司负责。

**三、先保证程序的正确性，防止过度工程**

> 1.先把眼前的问题解决掉，解决好，再考虑将来的扩展问题。  
> 2.先写出可用的代码，反复推敲，再考虑是否需要重用的问题。  
> 3.先写出可用，简单，明显没有bug的代码，再考虑测试的问题。

### 通用规范

#### 空格

尽量多用空格、空行让代码结构好看一些；

#### 变量

* 一个变量有且只有一个功能，尽量不要把一个变量用作多种用途;  
* 变量在使用前应初始化，防止未初始化的变量被引用;  
* 局部变量应该尽量接近使用它的地方;  

#### if语句

**1.必须列出所有分支（穷举所有的情况），而且每个分支都必须给出明确的结果。**  

推荐这样写： 
 
```
var hintStr;
if (count < 3) {
  hintStr = "Good";
} else {
  hintStr = "";
}
```

不推荐这样写：

```
var hintStr;
if (count < 3) {
 hintStr = "Good";
}
```

**2.不要使用过多的分支，要善于使用return来提前返回错误的情况。**

**3.条件表达式如果很长，则需要将他们提取出来赋给一个BOOL值。**

**4.条件语句的判断应该是变量在左，常量在右。**

**5.每个分支的实现代码都必须被大括号包围。**

推荐这样写：

```
if (!error) {
  return success;
}
```

**6.条件过多，过长的时候应该换行**

推荐这样写：

```
if (condition1() && 
    condition2() && 
    condition3() && 
    condition4()) {
  // Do something
} 

```

不推荐这样写：

```
if (condition1() && condition2() && condition3() && condition4()) {
  // Do something
}
```

#### for语句

**1.不可在for循环内修改循环变量，防止for循环失去控制。**  
**2.尽量避免使用continue和break。**

#### switch分支  

**1.每个分支都必须用大括号括起来。**  

推荐这样写：  

```
switch (integer) {  
  case 1:  {
    // ...  
   }
    break;  
  case 2: {  
    // ...  
    break;  
  }  
  case 3: {
    // ...  
    break; 
  }
  default:{
    // ...  
    break; 
  }
}

```
  
**2.使用枚举类型时，不能有default分支， 除了使用枚举类型以外，都必须有default分支。**

```
RWTLeftMenuTopItemType menuType = RWTLeftMenuTopItemMain;  
switch (menuType) {  
  case RWTLeftMenuTopItemMain: {
    // ...  
    break; 
   }
  case RWTLeftMenuTopItemShows: {
    // ...  
    break; 
  }
  case RWTLeftMenuTopItemSchedule: {
    // ...  
    break; 
  }
}

```

在Switch语句使用枚举类型的时候，如果使用了default分支，在将来就无法通过编译器来检查新增的枚举类型了。

#### 函数

**1.一个函数的长度必须限制在50行以内**  
**2.一个函数只做一件事（单一原则）**  
**3.对于有返回值的函数（方法），每一个分支都必须有返回值**  
**4.对输入参数的正确性和有效性进行检查，参数错误立即返回**  
**5.如果在不同的函数内部有相同的功能，应该把相同的功能抽取出来单独作为另一个函数**   
**6.将函数内部比较复杂的逻辑提取出来作为单独的函数** 

### OC规范

#### 变量

**1.变量名必须使用驼峰格式**

类，协议使用大驼峰：  

```
HomePageViewController.h
<HeaderViewDelegate>
```

对象等局部变量使用小驼峰：  

```
NSString *personName = @"";
NSUInteger totalCount = 0;
```

**2.变量的名称必须同时包含功能与类型**

```
UIButton *addBtn //添加按钮
UILabel *nameLbl //名字标签
NSString *addressStr//地址字符串
```

**3.系统常用类作实例变量声明时加入后缀**

| 类型 | 后缀 |
| ------- | ------- |
| UIViewController | VC |
| UIView | View | 
| UILabel | Lbl |
| UIButton | Btn |
| UIImage | Img |
| UIImageView | ImagView |
| NSArray | Array |
| NSMutableArray | Marray |
| NSDictionary | Dict |
| NSMutableDictionary | Mdict |
| NSString | Str |
| NSMutableString | Mstr |
| NSSet | Set |
| NSMutableSet | Mset |

#### 常量

**1.常量以相关类名作为前缀**

推荐这样写：  

```
static const NSTimeInterval ZOCSignInViewControllerFadeOutAnimationDuration = 0.4;
```  

不推荐这样写：  

```
static const NSTimeInterval fadeOutTime = 0.4;
```

**2.建议使用类型常量，不建议使用#define预处理命令**  

首先比较一下这两种声明常量的区别：

* 预处理命令：简单的文本替换，不包括类型信息，并且可被任意修改。
* 类型常量：包括类型信息，并且可以设置其使用范围，而且不可被修改。  

使用预处理虽然能达到替换文本的目的，但是本身还是有局限性的：    

* 不具备类型信息。
* 可以被任意修改。

**3.对外公开某个常量**

推荐这样写：  

```
//头文件
extern NSString *const ZOCCacheControllerDidClearCacheNotification;
```  

```
//实现文件
static NSString * const ZOCCacheControllerDidClearCacheNotification = @"ZOCCacheControllerDidClearCacheNotification";
static const CGFloat ZOCImageThumbnailHeight = 50.0f;
```

不推荐这样写：  

```
#define CompanyName @"Apple Inc." 
#define magicNumber 42 
```

#### 宏

**1.宏、常量名都要使用大写字母，用下划线‘_’分割单词。**  
  
```
#define URL_GAIN_QUOTE_LIST @"/v1/quote/list"
#define URL_UPDATE_QUOTE_LIST @"/v1/quote/update"
#define URL_LOGIN  @"/v1/user/login”
```  
**2.宏定义中如果包含表达式或变量，表达式和变量必须用小括号括起来。**  

```
#define MY_MIN(A, B)  ((A)>(B)?(B):(A))
```

#### CGRect函数

推荐这样写：  

```
CGRect frame = self.view.frame; 
CGFloat x = CGRectGetMinX(frame); 
CGFloat y = CGRectGetMinY(frame); 
CGFloat width = CGRectGetWidth(frame); 
CGFloat height = CGRectGetHeight(frame); 
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```  

而不是  

```
CGRect frame = self.view.frame;  
CGFloat x = frame.origin.x;  
CGFloat y = frame.origin.y;  
CGFloat width = frame.size.width;  
CGFloat height = frame.size.height;  
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

#### Block

**为常用的Block类型创建typedef**  

```
typedef int(^EOCSomeBlock)(BOOL flag, int value);

EOCSomeBlock block = ^(BOOL flag, int value){
     // Implementation
};
```

定义作为参数的Block：  

```
typedef void(^EOCCompletionHandler)(NSData *data, NSError *error);
- (void)startWithCompletionHandler:(EOCCompletionHandler)completion;”
```

通过typedef定义Block签名的好处是:如果要某种块增加参数，那么只修改定义签名的那行代码即可。

#### 属性

**1.属性的命名使用小驼峰**  

推荐这样写：  

```
@property (nonatomic, readwrite, strong) UIButton *confirmButton;
```

**2.属性的关键字推荐按照 原子性，读写，内存管理的顺序排列**  

推荐这样写：  

```
@property (nonatomic, readwrite, copy) NSString *name;
@property (nonatomic, readonly, copy) NSString *gender;
@property (nonatomic, readwrite, strong) UIView *headerView;
```

**3.Block属性应该使用copy关键字**  

推荐这样写：  

```
typedef void (^ErrorCodeBlock) (id errorCode,NSString *message);
@property (nonatomic, readwrite, copy) ErrorCodeBlock errorBlock;//将block拷贝到堆中
```

**4.形容词性的BOOL属性的getter应该加上is前缀**  

推荐这样写：  

```
@property (assign, getter=isEditable) BOOL editable;
```

**5.尽量使用不可变对象**  

建议尽量把对外公布出来的属性设置为只读，在实现文件内部设为读写。具体做法是：

* 在头文件中，设置对象属性为```readonly```。
* 在实现文件中设置为```readwrite```。

这样一来，在外部就只能读取该数据，而不能修改它，使得这个类的实例所持有的数据更加安全。而且，对于集合类的对象，更应该仔细考虑是否可以将其设为可变的。  

#### 方法  

**1.方法名中不应使用and，而且签名要与对应的参数名保持高度一致**  

推荐这样写：

```
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```  

不推荐这样写： 

```
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;
```

**2.方法实现时，如果参数过长，则令每个参数占用一行，以冒号对齐**  

```
- (void)doSomethingWith:(NSString *)theFoo
                   rect:(CGRect)theRect
               interval:(CGFloat)theInterval
{
   //Implementation
}
```

**3.私有方法应该在实现文件中申明**  

```
@interface ViewController ()
- (void)basicConfiguration;
@end

@implementation ViewController
- (void)basicConfiguration
{
   //Do some basic configuration
}
@end
```

**4.方法名用小写字母开头的单词组合而成**  

```
- (NSString *)descriptionWithLocale:(id)locale;
```

**5.方法名前缀**  

* 刷新视图的方法名要以```refresh```为首。
* 更新数据的方法名要以```update```为首。

推荐这样写：  

```
- (void)refreshHeaderViewWithCount:(NSUInteger)count;
- (void)updateDataSourceWithViewModel:(ViewModel*)viewModel;
```

#### 类  

**1.类的名称应该以三个大写字母为前缀；创建子类的时候，应该把代表子类特点的部分放在前缀和父类名的中间**  

推荐这样写：

```
//父类
ZOCSalesListViewController

//子类
ZOCDaySalesListViewController
ZOCMonthSalesListViewController
```

**2.initializer && dealloc**  

推荐：

* 将 dealloc 方法放在实现文件的最前面
* 将init方法放在dealloc方法后面。如果有多个初始化方法，应该将指定初始化方法放在最前面，其他初始化方法放在其后。

**2.1 dealloc方法里面应该直接访问实例变量，不应该用点语法访问**  

**2.2 init方法的写法：**  

* init方法返回类型必须是instancetype，不能是id。
* 必须先实现[super init]。

```
- (instancetype)init 
{ 
    self = [super init]; // call the designated initializer 
    if (self) { 
        // Custom initialization 
    } 
    return self; 
} 
```

**3.所有返回类对象和实例对象的方法都应该使用instancetype**  

将instancetype关键字作为返回值的时候，可以让编译器进行类型检查，同时适用于子类的检查，这样就保证了返回类型的正确性（一定为当前的类对象或实例对象）

推荐这样写：

```
@interface ZOCPerson
+ (instancetype)personWithName:(NSString *)name; 
@end 
```

不推荐这样写：

```
@interface ZOCPerson
+ (id)personWithName:(NSString *)name; 
@end 
```

**4.在类的头文件中尽量少引用其他头文件**  

**5.类的布局**  

```

#pragma mark - Life Cycle Methods
- (instancetype)init
- (void)dealloc

- (void)viewWillAppear:(BOOL)animated
- (void)viewDidAppear:(BOOL)animated
- (void)viewWillDisappear:(BOOL)animated
- (void)viewDidDisappear:(BOOL)animated

#pragma mark - Override Methods

#pragma mark - Intial Methods

#pragma mark - Network Methods

#pragma mark - Target Methods

#pragma mark - Public Methods

#pragma mark - Private Methods

#pragma mark - UITableViewDataSource  
#pragma mark - UITableViewDelegate  

#pragma mark - Lazy Loads

#pragma mark - NSCopying  

#pragma mark - NSObject  Methods
```

#### 分类  

**1.分类添加的方法需要添加前缀和下划线**  

推荐这样写：

```
@interface NSDate (ZOCTimeExtensions)
 - (NSString *)zoc_timeAgoShort;
@end 
```

不推荐这样写：

```
@interface NSDate (ZOCTimeExtensions) 
- (NSString *)timeAgoShort;
@end 
```

**2.把类的实现代码分散到便于管理的多个分类中**

一个类可能会有很多公共方法，而且这些方法往往可以用某种特有的逻辑来分组。我们可以利用Objecctive-C的分类机制，将类的这些方法按一定的逻辑划入几个分类中。

#### 单例  

**1.单例不能作为容器对象来使用**  

单例对象不应该暴露出任何属性，也就是说它不能作为让外部存放对象的容器。它应该是一个处理某些特定任务的工具，比如在iOS中的GPS和加速度传感器。我们只能从他们那里得到一些特定的数据。

**2.使用dispatch_once来生成单例**

推荐这样写：

```
+ (instancetype)sharedInstance 
{ 
 static id sharedInstance = nil; 
 static dispatch_once_t onceToken = 0;
       dispatch_once(&onceToken, ^{ 
  sharedInstance = [[self alloc] init];
  }); 
 return sharedInstance; 
} 
```

不推荐这样写：

```
+ (instancetype)sharedInstance 
{ 
 static id sharedInstance; 
 @synchronized(self) { 
 if (sharedInstance == nil) {  sharedInstance = [[MyClass alloc] init]; 
 } } 
 return sharedInstance; 
} 
```

#### NSArray& NSMutableArray  

**1.addObject之前要非空判断。**

**2.取下标的时候要判断是否越界。**

**3.取第一个元素或最后一个元素的时候使用firtstObject和lastObject**

#### NSCache  

**1.构建缓存时选用NSCache 而非NSDictionary**

**2.NSCache优于NSDictionary的几点：**  

* 当系统资源将要耗尽时，NSCache具备自动删减缓冲的功能。并且还会先删减“最久未使用”的对象。
* NSCache不拷贝键，而是保留键。因为并不是所有的键都遵从拷贝协议（字典的键是必须要支持拷贝协议的，有局限性）。
* NSCache是线程安全的：不编写加锁代码的前提下，多个线程可以同时访问NSCache。

#### NSNotification

**1.通知的名称**  

建议将通知的名字作为常量，保存在一个专门的类中：

```
// Const.h
extern NSString * const ZOCFooDidBecomeBarNotification

// Const.m
NSString * const ZOCFooDidBecomeBarNotification = @"ZOCFooDidBecomeBarNotification";
```

**2.通知的移除**  

通知必须要在对象销毁之前移除掉。