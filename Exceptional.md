## 泛型设计与标准库
### Iterator   GotW#18
    * 有效的数值，*e.end() 错误
    * 有效的寿命，
    * 有效的范围，first一定在last之前？
    * 有效的操作，--e.end() 是否有效。

### 定义一个无视大小写的字符串类  GotW#29
    *string类时一个typedef typedef basic_string<char, char_traits<char>, allocator<char> > string;
     自定义一个ci_char_trains<char> 继承char_traits<char> 实现无视大小写的内容。
     定义如下typedef: typedef typedef basic_string<char, ci_char_traits> ci_string;


### 最大可复用性的通用Containers  GotW#16
    成员函数模板非常易用。

### 临时变量  GotW#2
    * 函数参数通过拷贝传值，使用const& 代替传值
    * 使用先增（preincrement）代替后增（postincrement），后增会先本身+1返回未+1之前的副本。
    * 参数转换时产生临时对象，尽可能显示使用构造函数。
    * ！绝对不要在一个函数里写有多个return（可能构造一个临时对象最后返回，但是会有性能问题，返回临时对象引用更加危险）

### 使用标准库

### 异常处理的安全性 GotW#8
    

### 代码的复杂性 GotW#20

## class 的继承与设计

### Class技术 GotW#
    * 尽量复用程式码，标准库。
    * 避免隐式转换，使你的构造函数是explicit
    * 尽量以by const&方式避免by value 传递参数
    * 用a op= b 代替 a = a op b的形式。
    * 提供了摸个运算子的标准版本，请同时提供op=的形式，以后者的实现实现前者。
    * 1 一元运算符应该是members
      2 = [] () -> 必须为members
      3 assignment版必须 为members
      4 其他二元运算子为nonmenbers
    * operator+ 不应该修改this物件值，并且返回值应当是 const T；避免 a+b=c
    * operator<< operator>>应总是返回stream&
    * 后置式累加运算子（T++）应以前置式实现。

### 改写虚拟函数


### 绝不使用public继承，除非是 liskov is-a 和Works like-A 的关系。
    * 广泛使用Pimpl Idoim（Pimpl point impl）,遮掩实现细节。
    * 形成内聚，让代码有单一任务。

### 绝不要为了重复使用base class 的代码使用public继承，public继承是为了已有代码以多态方式重复运用base objects。

### 面向对象程式设计    GotW#13

### 编译器的依赖

## Traps,Pitfalls and Anti-Idioms
### Object Identity
    防止自赋值，指针的比较等。

### 