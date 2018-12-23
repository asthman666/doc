# Passing Reference-Type Parameters

一个引用类型的变量不直接包含它的数据；它包含的是一个指向它的数据的引用。


    class PassingRefByVal 
    {
        static void Change(int[] pArray)
        {
            pArray[0] = 888;  // This change affects the original element.
            pArray = new int[5] {-3, -1, -2, -3, -4};   // This change is local.
            System.Console.WriteLine("Inside the method, the first element is: {0}", pArray[0]);
        }

        static void Main() 
        {
            int[] arr = {1, 4, 5};
            System.Console.WriteLine("Inside Main, before calling the method, the first element is: {0}", arr [0]);

            Change(arr);
            System.Console.WriteLine("Inside Main, after calling the method, the first element is: {0}", arr [0]);
        }
    }
    /* Output:
        Inside Main, before calling the method, the first element is: 1
        Inside the method, the first element is: -3
        Inside Main, after calling the method, the first element is: 888
    */

一开始arr包含了指向{1, 4, 5}的引用
