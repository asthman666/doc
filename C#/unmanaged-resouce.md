# Cleaning Up Unmanaged Resources

The most common types of unmanaged resource are objects that wrap **operating system resources**, such as **files**, **windows**, **network connections**, or **database connections**. 

Although the garbage collector is able to track the lifetime of an object that encapsulates an unmanaged resource, it doesn't know how to release and clean up the unmanaged resource.

