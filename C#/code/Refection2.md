## Get the `private static` field value for class.

  Type type = typeof(TheClass);
  FieldInfo info = type.GetField(name, BindingFlags.NonPublic | BindingFlags.Static);
  object value = info.GetValue(null);
