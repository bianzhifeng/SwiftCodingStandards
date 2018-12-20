# SwiftCodingStandards
swift编码规范


# 1.格式规范

## 1.1. 尽量使用快捷键 ⌘⌥/ 进行代码注释, 而不是使用// 来注释.

### /// <#Description#>
### ///
### /// - Parameter testString: <#testString description#>
### /// - Returns: <#return value description#>

## 1.2. `ViewController`中使用`//MARK: -`按功能和协议分组.
* 注: MARK顺序没有强制要求，但System API & Public API一般分别放在第一块和第二块。*
大致区分为以下几块:
### // MARK: - Public
### // MARK: - Request
### // MARK: - Action
### // MARK: - Private
### // MARK: - Delegate

# 2.命名规范

## 2.1 常量尽量使用小写`k`字母开头
## 2.2 不要缩写简写命名, 如果一定要缩写那缩写的字母要全部大写.
## 2.3 不要使用含有歧义的单词
## 2.4 省略不必要的话语
## 2.5 如有必要, 可以通过补偿补类型信息来阐明参数的作用
如下: `forKeyPath `
`
func addObserver(_ observer: NSObject, forKeyPath path: String)
`
## 2.6 变量命名规则: 
### 2.6.1 使用小驼峰命名法, 首字母小写.
### 2.6.2 通过变量名应该能推断出该变量的作用及类型, 如果不能推断, 那么以变量类型结尾.

## 2.7 类型命名规则:
### 2.7.1 使用大坨峰命名法, 首字母大写.

## 2.8 方法命名规则:
### 2.8.1 简单明了: 如插入`insert(xx, at: xx)`
### 2.8.2 必要的动词短语: 如`make`代表创建 `get`代表获取 `move`等
### 2.8.3 如果每个参数都能构成独立短语时, 把介词提前, 如: `moveTo(x: a, y: b)`
### 2.8.4 当第一个参数构成语句的一部分时, 省略第一个参数标签, 否则添加第一个参数标签, 如`x.addSubView(y)` 与 `v.dismiss(animated: true)`

## 2.9 `Bool`类型命名使用`is`作为前缀
## 2.10 枚举定义不要包含类型前缀

## 2.11 协议命名
### 2.11.1 如果协议描述的是协议做的事应该命名为名词
### 2.11.2 如果协议描述的是能力, 需添加后缀`able` 或者 `ing`, 如`Equatable`与`ProgressReporting`
### 2.11.3 如果已经定义了类, 需要给类定义相关的协议, 则添加`Protocol`后缀

# 3.语法规范

## 3.1 能使用`let` 就不使用`var`
## 3.2 尽量少用`!`强制解包
## 3.3 可选类型拆包 使用 `if let / guard let else`
## 3.4 不要使用 `as! try!`, 与`if let `配合使用.
## 3.5 尽可能把常量定义在Type类型内部, 避免污染全局命名空间.
## 3.6 当实现Protocol时, 如果确定Protocol的实现不会被重写, 建议使用extension将Protocol实现分离, 如下:
`
class MyViewController: UIViewController {
  // class stuff here
}
// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source methods
}
// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
`
## 3.7 遵循最短路径原则.
## 3.8 在闭包内避免循环引用推荐写法:
`
resource.request().onComplete { [weak self] response in
    guard let strongSelf = self else { 
        return 
    }
    let model = strongSelf.updateModel(response)
    strongSelf.updateUI(model)
}
`

# 4.访问控制

## 4.1 对于私有访问, 如果在文件内不能被修改, 则标记为`private`, 如果在文件内可修改, 则标记为`fileprivate`
## 4.2 对于公有访问, 如果不希望在外面继承或者被重写, 则标记为`public`, 否则标记为`open`
