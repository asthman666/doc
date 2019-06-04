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

## 传递可变数量的参数

    static int Add(params int[] values) {
        int sum = 0;
        if (values != null) 
        {
            foreach ( var i in values ) 
            {
                sum += i;
            }
        }
        return sum;
    }

    static void Main() {
        Add(1,2,3); // 编译器会构造和初始化一个数组来容纳这些实参，会构造 new int[3]{1,2,3}
        Add(); // new int[0]
        Add(null); // 不会分配数组
    }

因为分配数组，数组在堆上分配，数组元素必须初始化，堆上数据会垃圾回收，因此对性能有一定的影响。可以考虑定义几个没有使用`params`关键字的重载方法。例如System.String的Concat方法。

## 参数和返回类型的规范

声明方法参数类型时，应尽量指定最弱的类型。

`IEnumerable<T>`, `IList<T>`, `ICollection<T>`, `List<T>`

一般将方法的返回类型声明为最强的类型，确保调用者使用方法返回值时的适用范围更大。

有时在不影响调用者的前提下修改方法的内部实现，可以选择一个较弱的返回类型。 `IList<T>` -> `ICollection<T>` -> `IEnumerable<T>`，如果一个方法返回`List<String>`，考虑到以后可能返回`String[]`，可以考虑将方法的返回值修改为`IList<string>`。
