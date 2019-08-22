List的一个构造方法

    public List(IEnumerable<T> collection)
    {
      if (collection == null)
        ThrowHelper.ThrowArgumentNullException(ExceptionArgument.collection);

      // IEnumerable<T> 可以直接 as 到 ICollection<T>    
      // 然后可以直接调用 Count 和 CopyTo 方法
      // objs 可能为 null， 如果传入的 collection 没有实现 ICollection<T> 的时候
      ICollection<T> objs = collection as ICollection<T>;
      if (objs != null)
      {
        int count = objs.Count;
        if (count == 0)
        {
          this._items = List<T>._emptyArray;
        }
        else
        {
          this._items = new T[count];
          objs.CopyTo(this._items, 0);
          this._size = count;
        }
      }
      else
      {
        this._size = 0;
        this._items = List<T>._emptyArray;
        foreach (T obj in collection)
          this.Add(obj);
      }
    }