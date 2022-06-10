## Using Constructors 

### Using the base keyword

    public class Employee
    {
        public int Salary;

        public Employee() { }

        public Employee(int annualSalary)
        {
            Salary = annualSalary;
        }

        public Employee(int weeklySalary, int numberOfWeeks)
        {
            Salary = weeklySalary * numberOfWeeks;
        }
    }

A constructor can use the `base` keyword to call the constructor of a base class. For example:

    public class Manager : Employee
    {
        public Manager(int annualSalary)
            : base(annualSalary)
        {
            //Add further instructions here.
        }
    }    

In this example, the constructor for the base class is called before the block for the constructor is executed.     

In a derived class, if a base-class constructor isn't called explicitly by using the base keyword, the parameterless constructor, if there's one, is called implicitly. This means that the following constructor declarations are effectively the same:

    public Manager(int initialData)
    {
        //Add further instructions here.
    }

    public Manager(int initialData)
        : base()
    {
        //Add further instructions here.
    }    

If a base class doesn't offer a parameterless constructor, the derived class must make an explicit call to a base constructor by using base.    

### Using the this keyword

A constructor can invoke another constructor in the same object by using the `this` keyword. For example, the second constructor in the previous example can be rewritten using this:

    public Employee(int weeklySalary, int numberOfWeeks)
        : this(weeklySalary * numberOfWeeks)
    {
    }

The use of the this keyword in the previous example causes this constructor to be called:

    public Employee(int annualSalary)
    {
        Salary = annualSalary;
    }    

## How to create user-defined exceptions

1. Create a serializable class that inherits from Exception. The class name should end in "Exception":

        [Serializable]
        public class StudentNotFoundException : Exception { }

2. Add the default constructors:

        [Serializable]
        public class StudentNotFoundException : Exception
        {
            public StudentNotFoundException() { }

            public StudentNotFoundException(string message)
                : base(message) { }

            public StudentNotFoundException(string message, Exception inner)
                : base(message, inner) { }
        }        

3. Define any additional properties and constructors:

        [Serializable]
        public class StudentNotFoundException : Exception
        {
            public string StudentName { get; }

            public StudentNotFoundException() { }

            public StudentNotFoundException(string message)
                : base(message) { }

            public StudentNotFoundException(string message, Exception inner)
                : base(message, inner) { }

            public StudentNotFoundException(string message, string studentName)
                : this(message)
            {
                StudentName = studentName;
            }
        }    

4. You have created a custom exception, and you can throw it anywhere with code like the following:

        throw new StudentNotFoundException("The student cannot be found.", "John");

        


