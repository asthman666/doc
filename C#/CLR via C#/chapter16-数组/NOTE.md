所有数组都隐式的从System.Array抽象类派生，后者又派生自System.Object，所以数组始终是引用类型，是在托管堆中分配的。

### 多维数组

    int[,] myInts = new Int[10,20];

    string[,,] myStrings = new String(10,2,5);

### 初始化数组

    String[] names = new String[] {"Beata", "Noah"};

    var countries = new String[] {"China", "USA"};

    var cities = new[] {"Beijing", "ShangHai", "HongKong"};

    String[] brands = {"Nike", "Starbuck"};

### 数组转型


