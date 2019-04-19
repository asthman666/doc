# String

    public sealed class String : IComparable, ICloneable, IConvertible, IEnumerable, IComparable<string>, IEnumerable<char>, IEquatable<string>
    {
        private static unsafe bool EqualsHelper(string strA, string strB)
        {
        int length = strA.Length;
        fixed (char* chPtr1 = &strA.m_firstChar)
            fixed (char* chPtr2 = &strB.m_firstChar)
            {
                char* chPtr3 = chPtr1;
                char* chPtr4 = chPtr2;
                for (; length >= 12; length -= 12)
                {
                    if (*(long*) chPtr3 != *(long*) chPtr4 || *(long*) (chPtr3 + 4) != *(long*) (chPtr4 + 4) || *(long*) (chPtr3 + 8) != *(long*) (chPtr4 + 8))
                    return false;
                    chPtr3 += 12;
                    chPtr4 += 12;
                }
                for (; length > 0 && *(int*) chPtr3 == *(int*) chPtr4; length -= 2)
                {
                    chPtr3 += 2;
                    chPtr4 += 2;
                }
                return length <= 0;
            }
        }

        public static bool Equals(string a, string b)
        {
            if ((object) a == (object) b)
                return true;
            if (a == null || b == null || a.Length != b.Length)
                return false;
            return string.EqualsHelper(a, b);
        }

        public static bool operator ==(string a, string b)
        {
            return string.Equals(a, b);
        }

        public override bool Equals(object obj)
        {
            if (this == null)
                throw new NullReferenceException();
            string strB = obj as string;
            if (strB == null)
                return false;
            if ((object) this == obj)
                return true;
            if (this.Length != strB.Length)
                return false;
            return string.EqualsHelper(this, strB);
        }

        public bool Equals(string value)
        {
            if (this == null)
                throw new NullReferenceException();
            if (value == null)
                return false;
            if ((object) this == (object) value)
                return true;
            if (this.Length != value.Length)
                return false;
            return string.EqualsHelper(this, value);
        }
    }

* `String`类重载了`==`操作符，`==`比较的是字符串本身
* `String`重写了`object`类的`bool Equals(object obj)`方法，`Equals`比较的是字符串本身
* 如果要比较`String`的引用，可以使用

        string ss1 = "N";
        string ss2 = "N";
        bool eq = (Object)ss2 == (Object)ss1;

    或者

        Object.ReferenceEquals(ss1, ss2)

        // Object class some source code
        public class Object
        {
            public virtual bool Equals(object obj)
            {
                return RuntimeHelpers.Equals(this, obj);
            }

            public virtual int GetHashCode()
            {
                return RuntimeHelpers.GetHashCode(this);
            }
            
            public static bool Equals(object objA, object objB)
            {
                if (objA == objB)
                    return true;
                if (objA == null || objB == null)
                    return false;
                return objA.Equals(objB);
            }

            public static bool ReferenceEquals(object objA, object objB)
            {
                return objA == objB;
            }  
        }
      
* 如果一个类没有重载`==`，那么默认使用`object`的`==`
