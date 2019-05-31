## 默认参数

    private static void M(int x = 9, string s = "A", DateTime = dafault(DateTime), Guid guid = new Guid()){}

    private static void N(int x, string y){}

    M();

    M(8, "X");

    M(5, guid: Guid.NewGuid(), dt: DateTime.Now);

    M(s_n++, s_n++.ToString());

    M(s: (s_n++).ToString(), x: s_n++);

    N(y: "world", x: 1);

### 在方法中为部分参数指定默认值的原则

* 有默认值的参数必须放在没有默认值的所有参数之后。有一个例外，“参数数组”这种参数必须放在所有参数（包括有默认值的这些）之后，而且数组本身不能有一个默认值

* 默认值必须是编译时能确定的常量。

* 如果方法从模块外部调用，更改参数的默认值具有潜在的危险性。call site在它的调用中**嵌入**默认值。所以更改参数的默认值，需要重新编译包含call site的代码。

### 调用具有可选参数的方法的原则

* 命名实参只能出现在实参列表的尾部

* 可按名称将实参传给没有默认值的参数

* 对于有默认值的参数，如果想省略它们的实参，以传参数名的方式传递实参即可

* 如果参数要求ref/out，有以下语法

        static void M(ref int x){}

        // call
        int a = 5;
        M(x: ref a);

## 隐式类型的局部变量

     var n = null; // Error, 编译器无法推断n的类型

不能用var声明方法的参数类型

不能用var声明类型中的字段

必须显示初始化用var声明的变量

## 传递引用

CLR默认所有的方法参数都传值
