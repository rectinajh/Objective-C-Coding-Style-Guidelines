# iOS编码规范

上海益生健康科技有限公司技术研发部 2013年9月3日

## 关于为了统一团队协作下代码的规范性、风格的统一性以及编程的注意点，而制定本规范。本规范仅作为建议推广使用，只要代码风格保持自身的规范性、风格的统一性，也是允许的。很多规范是语言通用的，有些是Objective-C特有的，本规范基于Apple编码规范、Xcode代码示例、Objective-C语言规范以及Java语言官方规范等文档，适用于使用Objective-C语言相关的工程。

## 术语* 大写驼峰式命名法——每个词首字符大写，其余字符均小写，如`AppDelegate`、`Global`、`DataTransfer`等；* 小写驼峰式命名法——除第一个词首字符小写外，其余词首字符大写，其他字符均小写，如`fileName`、`tempArray`、`titleLabel`等；
##编码规范### 一、格式排版* 使用等宽字体（如Xcode默认的Menlo Regular）而不是非等宽字体，利于视觉上的上下对齐；* 每行不超过100个字符，Xcode通过Preferences->Text Editing->Editing-> Page guide at column输入100来设置宽度提醒线；* 使用Tab缩进而非空格缩进，并且缩进宽度为4个字符，Xcode通过Preferences->Text Editing->Indentation，Prefer indent using选择Tabs，Tab width输入4，Indent width输入4来进行设置。* 单目运算符与操作数之间不留空，如`&`、`!`、`^`；双目运算符应与它们的操作数用1个空格分开；逗号和分号紧跟前面的语句，与后面的语句用1个空格分开；* 指针`*`与前面的数据类型留1个空格，紧贴后面的变量名；

**例如：**
```objc
NSString *password;
```

**而不是：**
```objc
NSString* password;
```

或者
```objc
NSString * password;
```
* 方法大括号和其它大括号（比如`for`、`if`、`while`、`switch`等等）应在语句的同一行开始，而在新的一行关闭；**例如：**
```objc
if (user.isHappy) {
    //Do something
} else {
    //Do something else
}
```

* 为避免错误，条件语句体必须使用大括号，即便语句体中的语句可以不必使用大括号（比如只有一行语句）；

**例如：**
```objc
if (!error) {
    return success;
}
```

**而不是：**
```objc
if (!error)
    return success;
```

或者
```objc
if (!error) return success;
```

* 三元运算子：仅当使用该运算子可以让代码显得更清晰易懂时方可使用三元运算子，更多情况下应使用条件语句；

**例如：**
```objc
result = a > b ? x : y;
```

**而不是**
```objc
result = a > b ? x = c > d ? c : d : y;
```

* 在方法声明中，在(`-`/`+`)符号与返回值之间留1个空格。此外，参数与前面的冒号不留空，方法段与之间留1个空格；

**例如：**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```

* 为保证视觉上的整洁和代码组织，在方法之间应摒弃大段的空白行，提供且仅提供一行空白。

### 二、工程组织* 工程Group组织尽量跟本地磁盘实际路径相一致，利于定位；* 工程Group名尽量跟相关功能名或模块名相一致。不推荐按照类型来组织，比如有些将视图控制器类放到一个Group，视图类放到另外的Group的做法；* 工程Group尽量使用中文名，利于辨识；* 工程Group组织可按照约定俗成的来，比如第三方框架放在`Libs`、`Utils`、`公共`等Group中，Bean类放在`Bean` Group中，公共的自定义类及其他放到专门的Group中，命名为`Global`或`XxxUtils`、`XxxTools`等；* 资源文件的组织应跟上面的文件一样，文件应使用有意义的英文命名，应能表达它的用法；应避免使用中文或汉语拼音，除非表达更清晰、更利于辨识。### 三、命名* 常量：  * 应避免在代码中出现字面常数或常字符串，使用超过一次的应以宏或全局常量来替代；
  * 优先使用全局常量而非宏，应使用`static`方式声明常量；
  
**例如：**
```objc
static NSString * const kNotificationLoggedIn;
```
  * 宏有两种方式命名，一是全部大写，并使用下划线连接各个部分，如`SCREEN_WIDTH`；或者以`k`开头，后面每个词首字符大写，其余小写，如`kAppKey`；  * 其他约定俗成的命名方式，字典数据的键使用形如`kXxxKey`的方式命名，通知名称使用形如`kNotificationXxx`的方式命名。* 变量：  * 变量采用小写驼峰式命名法；  * 对于特殊类型的变量，命名时可带上属性，如`NSArray`的变量命名为`xxxArray`，其他的如`xxxDictionary`，`xxxSize`，`xxxRect`等；  * 对于UI相关的变量，命名时要后缀以特定的控件名，如`UILabel`的变量命名为`xxxLabel`，其他的如`xxxButton`，`xxxTableView`，`xxxImageView`等；  * 除了循环控制内的变量可以使用约定俗成的`i`、`j`、`k`等之外，变量应使用非缩写的英文单词。

**例如：**
```objc
UIButton *settingsButton;
```

**而不是**
```objc
UIButton *setBtn;
```
* 方法：  * 方法采用小写驼峰式命名法；  * 方法的参数个数不宜超过4个，过多则考虑封装或重构，比如封装成`NSDictionary`格式；* 类、协议、分类等：  * 采用大写驼峰式命名法；  * 其他可参照Xcode默认生成文件。* 文件：  * 文件采用大写驼峰式命名法；  * 视图控制器相关的按照`XxxViewController`的方式命名；  * 分类使用父类+分类名来命名，如`UIImageView+AFNetworking.h`。* 杂项：  * 上面所有应使用有意义的英文命名，应能表达它的用法，避免使用汉语拼音；  * 推荐使用约定俗成的缩写，比如`app`（application），`bg`（background），`func`（function），`info`（information），`init`（initialize），`max`（maximum），`min`（minimum），`msg`（message），`rect`（rectangle），`temp`（temporary）等；  * 专有名词保持通用的大小写格式，要么全部大写，要么全部小写，比如`XML`、`HTML`、`URL`、`HTTP`、`FTP`、`JPG`、`PNG`、`GIF`、`RGB`等。## 编码实践* 点表示法仅用于获取和改变属性，获取和改变属性同样仅用点表示法，括号表示法用于其他情况。
**例如：**
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**而不是：**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```* 警告应该尽量解决掉，但也不必开启Treat Warnings as Errors，因为有些警告还是无法解决的。* 不推荐处处都是注释，好的代码应该自解释。关键的逻辑、跳转、判断，以及复杂的算法，非常有必要使用注释。多个注释应尽量左对齐。
* 因为`nil`将被解析为`NO`，因此没有必要在条件语句中进行比较。永远不要将任何东西和`YES`进行直接比较，因为`YES`被定义为1，而一个`BOOL`变量可以有8个字节。

**例如：**
```objc
if (!someObject) {
}
```

**而不是：**
```objc
if (someObject == nil) {
}
```

**以下是BOOL变量的恰当用法：**
```objc
if (isAwesome)
if (![someObject boolValue])
```

**而不是**
```objc
if ([someObject boolValue] == NO)
if (isAwesome == YES)
```
* 方法的参数有效性检查；* 成员变量在初始化方法中不必设置为`0`或`nil`；* 使用`ARC`；* 分类明显的推荐使用`enum`来代替，而不是0、1、2……这样的字面数字* 使用MVC模式，减少层与层之间的耦合；* 回调的最佳方式是使用代理模式，而不是使用Notification；* `delegate`属性使用`weak`，防止循环引用；* 所有自定义的`Notification`名应统一在公共文件中命名，便于甄别重复；* 本地存储：单一对象可用归档，简单属性可用`NSUserDefaults`，多个相同类型的数据可用`SQLite`；使用`FMDB`框架；* 使用通用的、约定俗成的`alloc`和`init`的方式创建实例，而不是使用`new`方法；* 使用`#pragma mark – XXX`来区别不同的区块。* 在创建单例对象的共享实例时，应使用线程安全模式。
**例如：**```objc
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;
   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });
   return sharedInstance;
}
```
