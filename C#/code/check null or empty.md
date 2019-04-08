# Check Null Or Empty

一段源码

    using System.Data.Entity.Resources;

    namespace System.Data.Entity.Utilities
    {
        internal class Check
        {
            public static T NotNull<T>(T value, string parameterName) where T : class
            {
                if ((object) value == null)
                    throw new ArgumentNullException(parameterName);
                return value;
            }

            public static T? NotNull<T>(T? value, string parameterName) where T : struct
            {
                if (!value.HasValue)
                    throw new ArgumentNullException(parameterName);
                return value;
            }

            public static string NotEmpty(string value, string parameterName)
            {
                if (string.IsNullOrWhiteSpace(value))
                    throw new ArgumentException(Strings.ArgumentIsNullOrWhitespace((object) parameterName));
                return value;
            }
        }
    }

    string name = "";
    Check.NotEmpty(name, nameof(name));

    int? num = null;
    Check.NotNull(num, nameof(num));

    string str = null;
    Check.NotNull(str, nameof(str));

用到了泛型，泛型中用到了where 约束

用到了静态方法的重载

用到了class的internal

用到了nameof 获取变量的名字

判断参数直接throw Exception

