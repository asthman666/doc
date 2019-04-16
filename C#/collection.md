# Collection

## Array

    Object -> System.Array(abstract class)

`int[]`和`string[]`都继承于`System.Array`，`System.Array`是引用类型，因此数组也是引用类型

* 数组存在连续的内存上，因此插入和删除数据很不方便
* 数组定义必须指定大小

## ArrayList

    object[] _items

* object类型的数组的封装，创建不用指定大小，可以自动resize数组
* 添加和获取值类型会有装箱（数据从栈到堆）和拆箱（数据从堆到栈），性能有影响

## List<T>

    T[] _items;

* T类型数组的封装，创建不用指定大小，可以自动resize数组
* 无拆箱装箱，类型安全，相同逻辑不同类型的代码可以公用

##  LinkedList<T>
    public class LinkedList<T> 
    {
        internal LinkedListNode<T> head;
    }

    public sealed class LinkedListNode<T>
    {
        internal LinkedList<T> list;
        internal LinkedListNode<T> next;
        internal LinkedListNode<T> prev;
        internal T item;
        // ...
    }

链表的核心不是数组，是`LinkedListNode`，这个类有前一个节点，后一个节点，所以链表不需要分配在一段连续的内存上，它通过next或者prev可以找到所有元素

## Queue<T>

* 先进先出
* 内部是数组的实现

## Stack<T>

* 先进后出
* 内部是数组的实现

## 总结

* 根据数据结构说说优缺点，效率和内存方面，时间复杂度，空间复杂度等

