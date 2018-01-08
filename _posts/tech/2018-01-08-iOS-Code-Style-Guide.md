---
layout: post
title: iOS编码风格指南 
category: 技术
tags: iOS
description: iOS编码风格指南
--- 

### 前言

- 为了*`保持代码一致性`*和易于 *`Code Review`*，本文档整理了*`iOS`* 开发应遵循的基本规范。
	
- 本编码风格指南将用于*`iOS项目`*的**`Objective-C`**编码规范。


### 主要参考规范
### [*Google Objective-C Style Guide*](google.github.io/styleguide/objcguide.xml)

### [*The Objective-C Programming Language*](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html)

### [*iOS App Programming Guide*](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html)

### 语言
- 所有**`代码文件`**、**`资源文件`**均使用**`US英语`**

### 命名规则
- 小驼峰命名法，例如：*`userName`*

- 大驼峰命名法，例如：*`ProductDetailViewController`*

### 常量
- 常量是容易重复被使用和无需通过查找和代替就能快速修改值。常量应该使用*`static`*而不是使用*`#define`*，除非显示地使用宏。例如:
		
	```
	static CGFloat const kCommonFontSizeSmall_10 = 10.0f;
	
	static NSString * const CommonNotificationName = @"foo";
	```
	
### 字面值
- **`NSString`**、**`NSDictionary`**、**`NSArray`**和**`NSNumber`**的字面值应该在创建这些类的不可变实例时被使用。请特别注意*`nil`*值不能传入**`NSArray`**和**`NSDictionary`**字面值，因为这样会导致*`crash`*。

	```
	NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve",@"Paul"];	NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
	
	NSNumber *shouldUseLiterals = @YES;
	
	NSNumber *buildingStreetNumber = @10018;
	```
	
### 枚举
- 当使用**`enum`**时，推荐使用新的固定基本类型规则，因为它有更强的类型检查和代码补全。当前枚举使用*`NS_ENUM()`*		/**		 *
		 */		typedef NS_ENUM(NSUInteger, CustomTipType)		{			NoDataType = 0, //    			NoProductType //     
		};
		
### Block
- 使用*`Block`*时，内容四个空格缩进，`^`后带有参数时，参数与`{`之间有一个缩进：

		// 示例：
		// blocks are easily readable
		[UIView animateWithDuration:1.0 animations:^{
			// something
		} completion:^(BOOL finished) {
			// something
		}];
	
### 类、方法
- 类名首字母大写，方法首字母小写，方法中参数首字母小写。

- 尽量保证方法意思清晰明了，取值方法前不要加前缀*`get`*。

- *`init`*方法应该遵循*`Apple`*生产代码模板的命名规则，返回类型应该使用*`instancetype`*而不是*`id`*。

- 类构造方法被使用时，应该返回类型是*`instancetype`*而不是*`id`*。这样确保编译器正确地推断结果类型。

- 注意空格的使用，参数过多时可换行保持对齐。

- 实例变量声明时变量名前面加下划线`_`，局部变量不用加:
		
	```
	// 示例：
	// 类名示例   	@interface ProductDetailViewController : CustomBaseViewController
		//  属性示例
	@property (assign, getter=isEditable) BOOL editable;
		
	//   方法1示例  	- (void)selectedAtIndex:(NSUInteger)index;
		
	//    类构造方法示例    	+ (instancetype)initWithTitle:(NSString *)title						  message:(NSString *)message						 delegate:(id)target						 btnTitle:(NSString *)btnTitle;
	@end
	```
	```
	//init方法示例	- (instancetype)init {    	self = [super init];		if (self) {
			// ...		}		return self;	}
	```
	```
	// 实例变量实例 <a.m   > 
	@interface NoDataView () {
	
	//  是否开始倒计时      
	BOOL _isStartCountdown;
	}
	
	//  other property
	@end
	```
	```
	//  局部变量示例  
	int selectedBtnIndex = selectedIndex;
	```

### 代码组织
- 任意函数长度不得超过`80`行

- 任意行代码不能超过`80`字符

- 在每个方法的定义前留白一行

- 二元运算符和参数之间要有一个空格，如赋值号`=`左右各留一个空格

- 一元运算符和参数之间不放置空格，比如`！`非运算符，`&`按位与，`|`按位或。

- *`if`*、*`while`*、*`switch`*等括号的使用必须风格统一

	```
	// 示例：
	//  二元运算符 
	_selectedIndex = selectedIndex;		
	//  一元运算符
	BOOL isOpen = true; BOOL isOver = !isOver;
	
	//  三元运算符      
	NSInteger value = 5;
	
	result = (value != 0) ? x : y;
	
	BOOL isHorizontal = YES;
	
	result = isHorizontal ? x : y;
	```
	```
	// if 示例
	if (!isOver) {
	
		//  doSomething
	} else {
	
		//  doSomething
	}
	```
	```
	// for示例
	for (int index = 0; index < count; index++) {
	
		//  doSomething
	}
	```
	```
	// switch   
	switch (index) {
		case 1: {
		
			// doSomething
		}
		break;
		case 2: {
		
			// doSomething
		}
		break;
		default: {
		
			// doSomething
		}
		break;
	}
	```

- **`Block`** 回调中，最好使用单独的方法执行回调逻辑,并且使用宏引用*`self`*，*`Block`*回调尽量简单：
	
	```
	// 示例：
	GJWeakSelf;
	RequestService *service = [[RequestService alloc] init];
	```
	```
	[service setWithSuccessBlock:^(id requestService) {
		GJStrongSelf;
		// function 1
		if (strongSelf) {
			[strongSelf XXX];
		}
	} withErrorBlock:^(SFRequestError *SFError) {
		GJStrongSelf;
		// function 2
		if (strongSelf) {
			[strongSelf XXX];
		}
	} withFailureBlock:^{
		GJStrongSelf;
		// function 3
		if (strongSelf) {
			[strongSelf XXX];
		}
	}];
	```

### 方法选择
- 使用*`[]`*、*`index`*取数组元素时，一定需要先判断数组个数是否大于索引。

- 对于金额计算展示时，由于精度问题，请使用**`double`**，而不是使用*`float`*。

- 对于*`cell`*重用，当对它进行模型刷新时，对于有*`if`*的分支一定有*`else`*分支与之对应。
	
	```
	// 示例:
	if ([model.productBalance doubleValue] <= 0) {
		//  售罄
		self.statusImgView.hidden = NO;
	} else {
		// 未售罄
		self.statusImgView.hidden = YES;
	}
	```
- 对应*`字体`*、*`颜色`*等必要使用*`宏`*定义，避免直接上代码
- 对于需要响应点击的文字视图，优先使用*`UIButton`*类。避免使用*`UILabel`*类加手势。


### 注释
- 原则上遵循**`代码自注释原则`**，开发环境较复杂时，尽量保证每个小逻辑有必要的注释

- 代码注释的快捷键: **`option`** + **`command`** + **`/`**

- 逻辑模块与模块之间，使用*`#pragma mark`*来分割，方便阅读代码

### 其他Objective-C编码规范
- 如果本编码规范不符合你的口味，可以查看其他编码规范：
	*[*CocoaDevCentral*](http://cocoadevcentral.com/articles/000082.php)*
