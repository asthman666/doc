# Generic

类型安全

* 编译检查类型

代码清晰

* 不需要强制类型转换

性能更佳

* 不需要装箱拆箱

# Generic 中的 `out`
下面是一个泛型协变接口

    namespace System.Collections.Generic
    {
        public interface IEnumerable<out T> : IEnumerable
        {
            IEnumerator<T> GetEnumerator();
        }
    }

协变使你可以使用一个 `more derived type` 来替代 `generic parameter`

    List<string> lstr = new List<string>();
    List<object> lobj = new List<object>();
    lobj = lstr; // compile error

    IEnumerable<string> istr = new List<string>();
    IEnumerable<object> iobject = new List<object>();
    iobject = istr;

### 在泛型接口中，如果一个参数类型可以声明为协变，它需要满足下面的条件：

* 这个参数类型仅仅作为接口方法的返回类型，并且不被用作方法的参数类型
* 这个参数类型没有在接口方法中被用作泛型约束

> [out-generic-modifier](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/out-generic-modifier)