    // TKey 为键对象
    public bool ContainsKey(TKey key)
    {
      return this.FindEntry(key) >= 0;
    }    
    
    private int FindEntry(TKey key)
    {
      if ((object) key == null)
        ThrowHelper.ThrowArgumentNullException(ExceptionArgument.key);
      if (this.buckets != null)
      {
        // GetHashCode确定是哪个bucket
        int num = this.comparer.GetHashCode(key) & int.MaxValue;
        for (int index = this.buckets[num % this.buckets.Length]; index >= 0; index = this.entries[index].next)
        {
          // hasCode和Equals都需要返回true，才算找到这个TKey
          if (this.entries[index].hashCode == num && this.comparer.Equals(this.entries[index].key, key))
            return index;
        }
      }
      return -1;
    }

    // this.compare
    private static EqualityComparer<T> CreateComparer()
    {
      RuntimeType genericParameter = (RuntimeType) typeof (T);
      if ((Type) genericParameter == typeof (byte))
        return (EqualityComparer<T>) new ByteEqualityComparer();
      if (typeof (IEquatable<T>).IsAssignableFrom((Type) genericParameter))
        return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (GenericEqualityComparer<int>), genericParameter);
      if (genericParameter.IsGenericType && genericParameter.GetGenericTypeDefinition() == typeof (Nullable<>))
      {
        RuntimeType genericArgument = (RuntimeType) genericParameter.GetGenericArguments()[0];
        if (typeof (IEquatable<>).MakeGenericType((Type) genericArgument).IsAssignableFrom((Type) genericArgument))
          return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (NullableEqualityComparer<int>), genericArgument);
      }
      if (genericParameter.IsEnum)
      {
        switch (Type.GetTypeCode(Enum.GetUnderlyingType((Type) genericParameter)))
        {
          case TypeCode.SByte:
            return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (SByteEnumEqualityComparer<sbyte>), genericParameter);
          case TypeCode.Byte:
          case TypeCode.UInt16:
          case TypeCode.Int32:
          case TypeCode.UInt32:
            return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (EnumEqualityComparer<int>), genericParameter);
          case TypeCode.Int16:
            return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (ShortEnumEqualityComparer<short>), genericParameter);
          case TypeCode.Int64:
          case TypeCode.UInt64:
            return (EqualityComparer<T>) RuntimeTypeHandle.CreateInstanceForAnotherGenericParameter((RuntimeType) typeof (LongEnumEqualityComparer<long>), genericParameter);
        }
      }
      return (EqualityComparer<T>) new ObjectEqualityComparer<T>();
    }

    // ObjectEqualityComparer
    namespace System.Collections.Generic
    {
        [Serializable]
        internal class ObjectEqualityComparer<T> : EqualityComparer<T>
        {
            public override bool Equals(T x, T y)
            {
                if ((object) x != null)
                {
                    if ((object) y != null)
                    return x.Equals((object) y);
                    return false;
                }
                return (object) y == null;
            }

            public override int GetHashCode(T obj)
            {
                if ((object) obj == null)
                    return 0;
                return obj.GetHashCode();
            }

            internal override int IndexOf(T[] array, T value, int startIndex, int count)
            {
                int num = startIndex + count;
                if ((object) value == null)
                {
                    for (int index = startIndex; index < num; ++index)
                    {
                    if ((object) array[index] == null)
                        return index;
                    }
                }
                else
                {
                    for (int index = startIndex; index < num; ++index)
                    {
                    if ((object) array[index] != null && array[index].Equals((object) value))
                        return index;
                    }
                }
                return -1;
            }

            internal override int LastIndexOf(T[] array, T value, int startIndex, int count)
            {
                int num = startIndex - count + 1;
                if ((object) value == null)
                {
                    for (int index = startIndex; index >= num; --index)
                    {
                    if ((object) array[index] == null)
                        return index;
                    }
                }
                else
                {
                    for (int index = startIndex; index >= num; --index)
                    {
                    if ((object) array[index] != null && array[index].Equals((object) value))
                        return index;
                    }
                }
                return -1;
            }

            public override bool Equals(object obj)
            {
                return obj is ObjectEqualityComparer<T>;
            }

            public override int GetHashCode()
            {
                return this.GetType().Name.GetHashCode();
            }
        }
    }