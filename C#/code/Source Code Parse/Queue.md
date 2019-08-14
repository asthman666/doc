    using System.Diagnostics;
    using System.Runtime.InteropServices;
    using System.Threading;
    namespace System.Collections.Generic
    {
        /// <summary>Represents a first-in, first-out collection of objects.</summary>
        /// <typeparam name="T">Specifies the type of elements in the queue.</typeparam>
        [DebuggerTypeProxy(typeof (System_QueueDebugView<>))]
        [DebuggerDisplay("Count = {Count}")]
        [ComVisible(false)]
        [__DynamicallyInvokable]
        [Serializable] // 指明这个类可以序列化
        public class Queue<T> : IEnumerable<T>, IEnumerable, ICollection, IReadOnlyCollection<T>
        {
            private static T[] _emptyArray = new T[0]; //定义一个静态数组变量_emptyArray，包含零个元素
            private T[] _array; 
            private int _head; 
            private int _tail;
            private int _size;
            private int _version;
            [NonSerialized] // 指明_syncRoot不可以被序列化
            private object _syncRoot;
            private const int _MinimumGrow = 4;
            private const int _ShrinkThreshold = 32;
            private const int _GrowFactor = 200;
            private const int _DefaultCapacity = 4;

            /// <summary>Initializes a new instance of the <see cref="T:System.Collections.Generic.Queue`1" /> class that is empty and has the default initial capacity.</summary>
            [__DynamicallyInvokable]
            public Queue()
            {
                this._array = Queue<T>._emptyArray; // 无参构造器，直接把静态变量_emptyArray赋值给实例变量_array
            }

            /// <summary>Initializes a new instance of the <see cref="T:System.Collections.Generic.Queue`1" /> class that is empty and has the specified initial capacity.</summary>
            /// <param name="capacity">The initial number of elements that the <see cref="T:System.Collections.Generic.Queue`1" /> can contain.</param>
            /// <exception cref="T:System.ArgumentOutOfRangeException">
            /// <paramref name="capacity" /> is less than zero.</exception>
            [__DynamicallyInvokable]
            public Queue(int capacity)
            {
                if (capacity < 0)
                    ThrowHelper.ThrowArgumentOutOfRangeException(ExceptionArgument.capacity, ExceptionResource.ArgumentOutOfRange_NeedNonNegNumRequired);
                this._array = new T[capacity]; // 创建一个大小为capacity的数组并赋值给实例变量_array
                this._head = 0;
                this._tail = 0;
                this._size = 0;
            }

            /// <summary>Initializes a new instance of the <see cref="T:System.Collections.Generic.Queue`1" /> class that contains elements copied from the specified collection and has sufficient capacity to accommodate the number of elements copied.</summary>
            /// <param name="collection">The collection whose elements are copied to the new <see cref="T:System.Collections.Generic.Queue`1" />.</param>
            /// <exception cref="T:System.ArgumentNullException">
            /// <paramref name="collection" /> is <see langword="null" />.</exception>
            [__DynamicallyInvokable]
            public Queue(IEnumerable<T> collection)
            {
                if (collection == null)
                    ThrowHelper.ThrowArgumentNullException(ExceptionArgument.collection);
                this._array = new T[4]; // 创建一个大小为4的数组并赋值给实例变量_array
                this._size = 0;
                this._version = 0;
                // 循环collection中的元素，并且对每个元素调用Enqueu方法
                foreach (T obj in collection)
                    this.Enqueue(obj); 
            }

            /// <summary>Gets the number of elements contained in the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            /// <returns>The number of elements contained in the <see cref="T:System.Collections.Generic.Queue`1" />.</returns>
            [__DynamicallyInvokable]
            public int Count
            {
                [__DynamicallyInvokable] get
                {
                    // 返回_size变量作为Count
                    return this._size;
                }
            }

            [__DynamicallyInvokable]
            bool ICollection.IsSynchronized
            {
                [__DynamicallyInvokable] get
                {
                    return false;
                }
            }

            [__DynamicallyInvokable]
            object ICollection.SyncRoot
            {
                [__DynamicallyInvokable] get
                {
                    if (this._syncRoot == null)
                        Interlocked.CompareExchange<object>(ref this._syncRoot, new object(), (object) null);
                    return this._syncRoot;
                }
            }

            /// <summary>Removes all objects from the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            [__DynamicallyInvokable]
            public void Clear()
            {
                if (this._head < this._tail)
                {
                    Array.Clear((Array) this._array, this._head, this._size);
                }
                else
                {
                    Array.Clear((Array) this._array, this._head, this._array.Length - this._head);
                    Array.Clear((Array) this._array, 0, this._tail);
                }
                this._head = 0;
                this._tail = 0;
                this._size = 0;
                ++this._version;
            }

            /// <summary>Copies the <see cref="T:System.Collections.Generic.Queue`1" /> elements to an existing one-dimensional <see cref="T:System.Array" />, starting at the specified array index.</summary>
            /// <param name="array">The one-dimensional <see cref="T:System.Array" /> that is the destination of the elements copied from <see cref="T:System.Collections.Generic.Queue`1" />. The <see cref="T:System.Array" /> must have zero-based indexing.</param>
            /// <param name="arrayIndex">The zero-based index in <paramref name="array" /> at which copying begins.</param>
            /// <exception cref="T:System.ArgumentNullException">
            /// <paramref name="array" /> is <see langword="null" />.</exception>
            /// <exception cref="T:System.ArgumentOutOfRangeException">
            /// <paramref name="arrayIndex" /> is less than zero.</exception>
            /// <exception cref="T:System.ArgumentException">The number of elements in the source <see cref="T:System.Collections.Generic.Queue`1" /> is greater than the available space from <paramref name="arrayIndex" /> to the end of the destination <paramref name="array" />.</exception>
            [__DynamicallyInvokable]
            public void CopyTo(T[] array, int arrayIndex)
            {
                if (array == null)
                    ThrowHelper.ThrowArgumentNullException(ExceptionArgument.array);
                if (arrayIndex < 0 || arrayIndex > array.Length)
                    ThrowHelper.ThrowArgumentOutOfRangeException(ExceptionArgument.arrayIndex, ExceptionResource.ArgumentOutOfRange_Index);
                int length1 = array.Length;
                if (length1 - arrayIndex < this._size)
                    ThrowHelper.ThrowArgumentException(ExceptionResource.Argument_InvalidOffLen);
                int num = length1 - arrayIndex < this._size ? length1 - arrayIndex : this._size;
                if (num == 0)
                    return;
                int length2 = this._array.Length - this._head < num ? this._array.Length - this._head : num;
                Array.Copy((Array) this._array, this._head, (Array) array, arrayIndex, length2);
                int length3 = num - length2;
                if (length3 <= 0)
                    return;
                Array.Copy((Array) this._array, 0, (Array) array, arrayIndex + this._array.Length - this._head, length3);
            }

            [__DynamicallyInvokable]
            void ICollection.CopyTo(Array array, int index)
            {
                if (array == null)
                    ThrowHelper.ThrowArgumentNullException(ExceptionArgument.array);
                if (array.Rank != 1)
                    ThrowHelper.ThrowArgumentException(ExceptionResource.Arg_RankMultiDimNotSupported);
                if (array.GetLowerBound(0) != 0)
                    ThrowHelper.ThrowArgumentException(ExceptionResource.Arg_NonZeroLowerBound);
                int length1 = array.Length;
                if (index < 0 || index > length1)
                    ThrowHelper.ThrowArgumentOutOfRangeException(ExceptionArgument.index, ExceptionResource.ArgumentOutOfRange_Index);
                if (length1 - index < this._size)
                    ThrowHelper.ThrowArgumentException(ExceptionResource.Argument_InvalidOffLen);
                int num = length1 - index < this._size ? length1 - index : this._size;
                if (num == 0)
                    return;
                try
                {
                    int length2 = this._array.Length - this._head < num ? this._array.Length - this._head : num;
                    Array.Copy((Array) this._array, this._head, array, index, length2);
                    int length3 = num - length2;
                    if (length3 <= 0)
                    return;
                    Array.Copy((Array) this._array, 0, array, index + this._array.Length - this._head, length3);
                }
                catch (ArrayTypeMismatchException ex)
                {
                    ThrowHelper.ThrowArgumentException(ExceptionResource.Argument_InvalidArrayType);
                }
            }

            /// <summary>Adds an object to the end of the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            /// <param name="item">The object to add to the <see cref="T:System.Collections.Generic.Queue`1" />. The value can be <see langword="null" /> for reference types.</param>
            [__DynamicallyInvokable]
            public void Enqueue(T item)
            {
                // 当Queue的实例是调用无参构造器时，第一次添加的时候
                // this._size为0， this._array.Length为0
                if (this._size == this._array.Length)
                {
                    // this._array.Length为0， capacity为0
                    int capacity = (int) ((long) this._array.Length * 200L / 100L);
                    if (capacity < this._array.Length + 4)
                        // capacity赋值为4
                        capacity = this._array.Length + 4;
                    this.SetCapacity(capacity);
                }                
                this._array[this._tail] = item; // this._array[0] = item
                this._tail = (this._tail + 1) % this._array.Length; // this._tail = 1 % 4 => this._tail = 1
                ++this._size; // this._size 变为 1
                ++this._version;
            }

            /// <summary>Returns an enumerator that iterates through the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            /// <returns>An <see cref="T:System.Collections.Generic.Queue`1.Enumerator" /> for the <see cref="T:System.Collections.Generic.Queue`1" />.</returns>
            [__DynamicallyInvokable]
            public Queue<T>.Enumerator GetEnumerator()
            {
                return new Queue<T>.Enumerator(this);
            }

            [__DynamicallyInvokable]
            IEnumerator<T> IEnumerable<T>.GetEnumerator() // 未定义access modifier，默认private
            {
                return (IEnumerator<T>) new Queue<T>.Enumerator(this);
            }

            [__DynamicallyInvokable]
            IEnumerator IEnumerable.GetEnumerator() // 未定义access modifier，默认private
            {
                return (IEnumerator) new Queue<T>.Enumerator(this);
            }

            /// <summary>Removes and returns the object at the beginning of the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            /// <returns>The object that is removed from the beginning of the <see cref="T:System.Collections.Generic.Queue`1" />.</returns>
            /// <exception cref="T:System.InvalidOperationException">The <see cref="T:System.Collections.Generic.Queue`1" /> is empty.</exception>
            [__DynamicallyInvokable]
            public T Dequeue()
            {
                if (this._size == 0)
                    ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EmptyQueue);                
                T obj = this._array[this._head]; // 把this._array[this._head]赋值给obj
                this._array[this._head] = default (T); // 给this._array[this._head]赋值为default(T)
                this._head = (this._head + 1) % this._array.Length; // this._head 加 1
                --this._size; // this._size 减 1 
                ++this._version;
                return obj;
            }

            /// <summary>Returns the object at the beginning of the <see cref="T:System.Collections.Generic.Queue`1" /> without removing it.</summary>
            /// <returns>The object at the beginning of the <see cref="T:System.Collections.Generic.Queue`1" />.</returns>
            /// <exception cref="T:System.InvalidOperationException">The <see cref="T:System.Collections.Generic.Queue`1" /> is empty.</exception>
            [__DynamicallyInvokable]
            public T Peek()
            {
                if (this._size == 0)
                    ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EmptyQueue);
                return this._array[this._head]; // 返回this._array[this._head]
            }

            /// <summary>Determines whether an element is in the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            /// <param name="item">The object to locate in the <see cref="T:System.Collections.Generic.Queue`1" />. The value can be <see langword="null" /> for reference types.</param>
            /// <returns>
            /// <see langword="true" /> if <paramref name="item" /> is found in the <see cref="T:System.Collections.Generic.Queue`1" />; otherwise, <see langword="false" />.</returns>
            [__DynamicallyInvokable]
            public bool Contains(T item)
            {
                int index = this._head;
                int size = this._size;
                EqualityComparer<T> equalityComparer = EqualityComparer<T>.Default;
                while (size-- > 0)
                {
                    if ((object) item == null)
                    {
                        if ((object) this._array[index] == null)
                            return true;
                    }
                    else if ((object) this._array[index] != null && equalityComparer.Equals(this._array[index], item))
                        return true;
                    index = (index + 1) % this._array.Length;
                }
                return false;
            }

            internal T GetElement(int i)
            {
                return this._array[(this._head + i) % this._array.Length];
            }

            /// <summary>Copies the <see cref="T:System.Collections.Generic.Queue`1" /> elements to a new array.</summary>
            /// <returns>A new array containing elements copied from the <see cref="T:System.Collections.Generic.Queue`1" />.</returns>
            [__DynamicallyInvokable]
            public T[] ToArray()
            {
                T[] objArray = new T[this._size];
                if (this._size == 0)
                    return objArray;
                if (this._head < this._tail)
                {
                    Array.Copy((Array) this._array, this._head, (Array) objArray, 0, this._size);
                }
                else
                {
                    Array.Copy((Array) this._array, this._head, (Array) objArray, 0, this._array.Length - this._head);
                    Array.Copy((Array) this._array, 0, (Array) objArray, this._array.Length - this._head, this._tail);
                }
                return objArray;
            }

            private void SetCapacity(int capacity)
            {
                // 创建大小为capacity的数组
                T[] objArray = new T[capacity];

                // this._size为0
                if (this._size > 0)
                {
                    if (this._head < this._tail)
                    {
                        // 拷贝this._array到objArray，从this._array的this._head开始，到objArray的0开始，大小为this._size
                        Array.Copy((Array) this._array, this._head, (Array) objArray, 0, this._size);
                    }
                    else
                    {
                        Array.Copy((Array) this._array, this._head, (Array) objArray, 0, this._array.Length - this._head);
                        Array.Copy((Array) this._array, 0, (Array) objArray, this._array.Length - this._head, this._tail);
                    }
                }
                this._array = objArray;
                this._head = 0;
                this._tail = this._size == capacity ? 0 : this._size;
                ++this._version;
            }

            /// <summary>Sets the capacity to the actual number of elements in the <see cref="T:System.Collections.Generic.Queue`1" />, if that number is less than 90 percent of current capacity.</summary>
            [__DynamicallyInvokable]
            public void TrimExcess()
            {                
                if (this._size >= (int) ((double) this._array.Length * 0.9))
                    return;
                // 重新给this._array分配成小一点的数组
                this.SetCapacity(this._size);
            }

            /// <summary>Enumerates the elements of a <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
            [__DynamicallyInvokable]
            [Serializable]
            // 一个结构，实现3个接口
            // 需要实现的方法有
            // bool MoveNext();
            // object Current { get; }
            // T Current {  get; }
            // void Reset();
            // void Dispose(); 
            public struct Enumerator : IEnumerator<T>, IDisposable, IEnumerator
            {
                private Queue<T> _q;
                private int _index; // 存储_currentElement是集合的第几个元素, base 0
                private int _version; 
                private T _currentElement; // 集合现在移动到的元素

                // 结构的构造方法, internal表示只有这个组建可以创建这个结构体
                internal Enumerator(Queue<T> q)
                {
                    this._q = q;
                    this._version = this._q._version;
                    this._index = -1;
                    this._currentElement = default (T);
                }

                /// <summary>Releases all resources used by the <see cref="T:System.Collections.Generic.Queue`1.Enumerator" />.</summary>
                [__DynamicallyInvokable]
                public void Dispose()
                {
                    this._index = -2;
                    this._currentElement = default (T);
                }

                /// <summary>Advances the enumerator to the next element of the <see cref="T:System.Collections.Generic.Queue`1" />.</summary>
                /// <returns>
                /// <see langword="true" /> if the enumerator was successfully advanced to the next element; <see langword="false" /> if the enumerator has passed the end of the collection.</returns>
                /// <exception cref="T:System.InvalidOperationException">The collection was modified after the enumerator was created. </exception>
                [__DynamicallyInvokable]
                public bool MoveNext()
                {
                    if (this._version != this._q._version)
                    ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumFailedVersion);
                    if (this._index == -2)
                        return false;
                    ++this._index; 
                    if (this._index == this._q._size) // 移动到元素最后一个元素的下一个元素了
                    {
                        this._index = -2;
                        this._currentElement = default (T);
                        return false;
                    }
                    this._currentElement = this._q.GetElement(this._index); // 把移动到的元素赋值给this._currentElement
                    return true;
                }

                /// <summary>Gets the element at the current position of the enumerator.</summary>
                /// <returns>The element in the <see cref="T:System.Collections.Generic.Queue`1" /> at the current position of the enumerator.</returns>
                /// <exception cref="T:System.InvalidOperationException">The enumerator is positioned before the first element of the collection or after the last element. </exception>
                [__DynamicallyInvokable]
                public T Current
                {
                    [__DynamicallyInvokable] get
                    {
                        if (this._index < 0)
                        {
                            if (this._index == -1)
                            ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumNotStarted);
                            else
                            ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumEnded);
                        }
                        return this._currentElement;
                    }
                }

                [__DynamicallyInvokable]
                // 接口的显示实现
                object IEnumerator.Current // 实现的接口的方法，可以是private
                {
                    [__DynamicallyInvokable] get
                    {
                    if (this._index < 0)
                        {
                            if (this._index == -1)
                                ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumNotStarted);
                            else
                                ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumEnded);
                        }
                        return (object) this._currentElement;
                    }
                }

                [__DynamicallyInvokable]
                void IEnumerator.Reset() // 实现的接口的方法，可以是private
                {
                    if (this._version != this._q._version)
                        ThrowHelper.ThrowInvalidOperationException(ExceptionResource.InvalidOperation_EnumFailedVersion);
                    this._index = -1;
                    this._currentElement = default (T);
                }
            }
        }
    }
