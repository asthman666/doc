    // Assembly location: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\System.Core.dll

    using System.Collections.Generic;

    namespace System.Linq
    {
        // Buffer 是个 struct
        internal struct Buffer<TElement>
        {
            // struct 包含一个数组引用类型
            internal TElement[] items;
            // struct 包含一个值类型
            internal int count;

            // struct 的构造方法
            internal Buffer(IEnumerable<TElement> source)
            {
                TElement[] array = (TElement[]) null;
                int length = 0;
                ICollection<TElement> elements = source as ICollection<TElement>;
                if (elements != null)
                {
                    length = elements.Count;
                    if (length > 0)
                    {
                    array = new TElement[length];
                    elements.CopyTo(array, 0);
                    }
                }
                else
                {
                    foreach (TElement element in source)
                    {
                    if (array == null)
                        array = new TElement[4];
                    else if (array.Length == length)
                    {
                        TElement[] elementArray = new TElement[checked (length * 2)];
                        Array.Copy((Array) array, 0, (Array) elementArray, 0, length);
                        array = elementArray;
                    }
                    array[length] = element;
                    ++length;
                    }
                }
                this.items = array;
                this.count = length;
            }

            internal TElement[] ToArray()
            {
                if (this.count == 0)
                    return new TElement[0];
                if (this.items.Length == this.count)
                    return this.items;
                TElement[] elementArray = new TElement[this.count];
                Array.Copy((Array) this.items, 0, (Array) elementArray, 0, this.count);
                return elementArray;
            }   
        }
    }
