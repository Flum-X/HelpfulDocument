### 命名规范

* 类名  
采用驼峰命名法，首字母大写, 示例：```HomeViewController ```

* 结构体名  
采用驼峰命名法，首字母大写, 示例：```Coupon```

* 变量名  
采用驼峰命名法，首字母小写, 示例：```pageNumber```

* 枚举名  
采用驼峰命名法，首字母大写, 示例：```OrderStatus ```

* 枚举值名  
采用驼峰命名法，首字母小写, 一般情况下一个单词就可以。示例：

```  
  enum OrderStatus: Int {
      case normal
      case expired
      case paid
  }
```

* 全局常量名  
采用驼峰命名法，首字母大写，并用小写的项目缩写名为前缀。如cc项目
  
```let ccAnimationDuration: TimeInterval = 0.25 ```

* 全局函数名  
采用驼峰命名法，首字母小写，并用小写的项目缩写名+下划线为前缀。cc项目示例：

```
func we_checkLogin() -> Bool {
   ...
}
```

* 协议名   
1.如果是单纯的协议，则采用驼峰命名法，首字母大写，后缀为"protocol"。示例：```SomeProtocol ```  
2.如果是用来做代理的，则采用驼峰命名法，首字母大写，后缀为"delegate"。示例：
```OrderCellDelegate```

* 协议方法名  
采用驼峰命名法，首字母小写。在创建一个代理方法时，第一个未命名的参数应该是代理源。 示例：  

```
  // 推荐：
  func namePickerView(_ namePickerView: NamePickerView, didSelectName name: String)
  func namePickerViewShouldReload(_ namePickerView: NamePickerView) -> Bool

  // 不推荐
  func didSelectName(namePicker: NamePickerViewController, name: String)
  func namePickerShouldReload() -> Bool
```

* 可选协议方法名  
使用```@objc```+```optional```关键字， 示例：  

```
@objc protocol OrderCellDelegate: class {
    // 除了自身对象之外，还有操作的控件作为参数
    func orderCell(cell: weOrderCell, didClick checkButton: UIButton)
    // 只有自身对象作为参数
    @objc optional func orderCellDidClickCheckButton(cell: weOrderCell)
}
```

* 资源文件名  
1.图片资源需要在名称中加上功能模块名，防止重复，示例：  
```img_home_right_arrow ```，```img_order_locate ```  
2.声音资源名称表明用途即可，示例：```qr_sound ```

* 闭包名  
要求同类名，但要以"closure"结尾，示例：```OrderViewClosure ```

* 扩展文件名  
1.文件中包含单个扩展，为类型 MyType 添加 MyProtocol 协议遵循，命名为 MyType+MyProtocol.swift。  
2.文件中包含多个扩展，为类型 MyType 添加协议遵循、嵌套类型或者其他功能的拓展，可以使用更通用的命名，只要它的前缀是 MyType+；例如，MyType+Additions.swift。

* 扩展方法名  
采用驼峰命名法，首字母小写，并用小写的项目缩写名+下划线为前缀。示例：

```
  extension UIView {
      /// 移除所有子控件
      func cc_removeAllSubviews() {
          ...
      }
  }
```

### 编码风格

* 尽可能的多用```let```，少用```var```
* 如果变量类型可以依靠推断得出，不建议声明变量时指明类型。示例：
  ```var name = "jack"```  
  
* 二元运算符(+, ==, 或->)的前后都需要添加空格，左小括号后面和右小括号前面不需要空格。
  
  ```
    let myValue = 20 + (30 / 2) * 3

  if 1 + 1 == 3 {
    fatalError("The universe is broken.")
  }

  func pancake() -> Pancake {
    ...
  }
  ```

* 逗号后面要加一个空格，示例：```var nums = [1, 2, 3, 4]```
* 左大括号不用另起一行，并与之前的元素相隔一个空格。

```
  class SomeClass {
    func someMethod() {
      if x == y {
        ...
      } else {
        ...
      }
    }
  }
```

* 尽量不使用```self.```，除非方法参数名与属性同名。
* 使用 // MARK: -按功能为一个文件中的代码分块, 下面一行保留为空行。示例：

```
  class Pirate {

    // MARK: - 实例属性

    private let pirateName: String

    // MARK: - 初始化

    init() {
        /* ... */
    }
  }
```
* 使用扩展来实现协议方法。示例：

```
  extension ViewController: OrderCellDelegate {

      func orderCell(cell: OrderCell, didClick checkButton: UIButton) {
          ...
      }
  }
```

* 使用```@available(iOS 10.0, *)```来标明起始系统版本号
* 尽可能避免使用强制转换和强制解包。
* 推荐把权限访问修饰符放到第一个位置。

```
  // 推荐
  private static let kMyPrivateNumber: Int
  // 不推荐
  static private let kMyPrivateNumber: Int
```

* 文档注释：使用每行前面三个斜杠（///）的格式。示例：

```
/// Returns the numeric value of the given digit represented as a Unicode scalar.
///
/// - Parameters:
///   - digit: The Unicode scalar whose numeric value should be returned.
///   - radix: The radix, between 2 and 36, used to compute the numeric value.
/// - Returns: The numeric value of the scalar.
func numericValue(of digit: UnicodeScalar, radix: Int = 10) -> Int {
  // ...
}
```

### 语法规范

* 访问等级：给文件级别的扩展指定显式访问等级是不允许的。拓展里的每一个成员如果不采用默认的访问等级，则应该单独进行指定。
  
推荐：  

```
extension String {
  public var isUppercase: Bool {
    // ...
  }

  public var isLowercase: Bool {
    // ...
  }
}
```

不推荐：

```
public extension String {
  var isUppercase: Bool {
    // ...
  }

  var isLowercase: Bool {
    // ...
  }
}
```

* 嵌套和命名空间：Swift 里允许嵌套 enum、struct 和 class，嵌套更适合（比起命名约定）表示作用域和类型之间的分级关系，因此推荐使用。

```
class Parser {
  enum Error: Swift.Error {
    case invalidToken(String)
    case unexpectedEOF
  }

  func parse(text: String) throws {
    // ...
  }
}
```

* for-where 循环：当整个 for 循环体只包含对元素的条件检查 if 块，可以将该检查放在 for 语句的 where 分句中。

推荐：

```
for item in collection where item.hasProperty {
  // ...
}
```
不推荐

```
for item in collection {
  if item.hasProperty {
    // ...
  }
}
```

* 只读计算属性的 get 块可以省略，将执行体直接嵌套在属性声明里。

推荐：

```
var totalCost: Int {
  return items.sum { $0.cost }
}
```

不推荐：

```
var totalCost: Int {
  get {
    return items.sum { $0.cost }
  }
}
```

* 使用显式类型和空集合。类型在赋值操作符的左边，空实例在赋值操作符的右边。
  
推荐这样写：  
  
```
  var x: [String: Int] = [:]
  var y: [Double] = []
  var z: Set<String> = []
  var mySet: MyOptionSet = []
```
不推荐这样写：

```
  var x = [String: Int]()
  var y = [Double]()
  var z = Set<String>()
  var mySet = MyOptionSet()
```

* 可选类型拆包时，使用```if let```或```guard let```判断。
* 多个可选类型拆包取值时，将多个if let或guard let判断合并。示例：

```
  if let name = person.name, 
  	let age = person.age {
  	
  }
```

* 尽量不要使用```as!```或```try!```，使用```if let as?```判断。示例：

```
  if let name = person.name as? String {
  
  }
```

* 跨多行函数声明缩进时，参数名左对齐（不是冒号对齐）。示例：

```
  func myFunctionWithManyParameters(parameterOne: String,
                                    parameterTwo: String,
                                    parameterThree: String) {

      print("\(parameterOne) \(parameterTwo) \(parameterThree)"
  }
```

* 基本上不要通过下标直接访问数组内容，如果可能使用如 ```.first``` 或 ```.last```, 因为这些方法是非强制类型并不会崩溃。(如果需要通过下标访问数组内容，在使用前要做边界检查)
* 推荐尽可能使用 ```for item in items``` 而不是 ```for i in 0..<items.count``` 遍历数组。
* 在解析可选类型时，推荐使用```guard```语句，而不是```if```语句，因为```guard```语句可以减少不必要的嵌套缩进。示例：

```
  // 推荐
  guard let monkeyIsland = monkeyIsland else {
      return
  }
  bookVacation(onIsland: monkeyIsland)
  bragAboutVacation(onIsland: monkeyIsland)

  // 不推荐
  if let monkeyIsland = monkeyIsland {
      bookVacation(onIsland: monkeyIsland)
      bragAboutVacation(onIsland: monkeyIsland)
  }

  // 禁止
  if monkeyIsland == nil {
      return
  }
  bookVacation(onIsland: monkeyIsland!)
  bragAboutVacation(onIsland: monkeyIsland!)
```

* 如果需要在2个状态间做出选择，建议使用```if```语句，而不是使用```guard```语句。

```
  // 推荐
  if isFriendly {
      print("你好, 远路来的朋友！")
  } else {
      print("穷小子, 哪儿来的?")
  }

  // 不推荐
  guard isFriendly else {
      print("穷小子, 哪儿来的?")
      return
  }
  print("你好, 远路来的朋友!")
```

* 其它情况建议优先使用```guard```语句
* 使用类型推断上下文，使用编译器推断上下文来编写简洁的代码。

```
  // 推荐
  let selector = #selector(viewDidLoad)
  view.backgroundColor = .red
  let toView = context.view(forKey: .to)
  let view = UIView(frame: .zero)

  // 不推荐
  let selector = #selector(ViewController.viewDidLoad)
  view.backgroundColor = UIColor.red
  let toView = context.view(forKey: UITransitionContextViewKey.to)
  let view = UIView(frame: CGRect.zero)
```

* 将错误抛出而不是随着返回值返回，可以更清晰地将问题从 API 里分离。合法输入和合法状态在结果域里产生合法输出，并通过标准的控制流进行处理。非法输入和非法状态应视作错误，并使用相关语法结构进行处理（do-catch 和 try）。例如：

```
struct Document {
  enum ReadError: Error {
    case notFound
    case permissionDenied
    case malformedHeader
  }

  init(path: String) throws {
    // ...
  }
}

do {
  let document = try Document(path: "important.data")
} catch Document.ReadError.notFound {
  // ...
} catch Document.ReadError.permissionDenied {
  // ...
} catch {
  // ...
}
```

### 网络请求

* 项目中的网络请求数据架构采用Alamofire + Moya + HandyJSON。
* 项目中处理网络请求的类，统一命名为: 'xxService'，比如‘HomeService’。
* 用来解析数据的模型优先使用```Struct```，```Struct```不能满足要求时，才使用```Class```。


