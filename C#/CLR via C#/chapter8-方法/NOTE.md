## 实力构造器和类

`.ctor` 构造器的IL代码

`.cctor` class constructor 类型构造器

如果类没有显示定义任何构造器，C#编译器将定义一个默认的无参构造器。

    public class SomeType {

    }

等于    

    public class SomeType {
        public SomeType() : base() {
            
        }
    }

如果基类没有提供无参构造器，那么派生类必须显示调用一个基类构造器，否则编译器会报错。

如果类的修饰符为`abstract`,那么编译器生成的默认构造器的可访问性就为`protected`;否则，构造器会被赋予`public`可访问性。

## 实例构造器和结构



