# Learn new C# concepts:

Access Modifiers:
1. Public – Visible in the current and referencing assembly.
2. Private – visible inside the current class.
3. Protected – Visible inside the current as well as in the derived class.
4. Internal – Visible inside the containing assembly.
5. Internal protected – Visible inside the containing assembly, also in the descendant of the current class.

* Sealed – The class stops inheriting any derived class.
* Static – The class contains only static members.
* Unsafe – The class that stores unsafe types like pointers.
* Abstract – No instance of the class if the Class is abstract.

## Types of Constructors in C#

* Default Constructor
* Parameterized Constructor
* Copy Constructor
* Private Constructor
* Static Constructor


1. Default Constructor
A default constructor is parameterless. If a class doesn't have a constructor then a default constructor gets called when object is created. The default constructor is added to a class by default if you don't add any constructor to your class. The default constructor should have public access.
```
using System;
namespace Studytonight
{
    public class Student
    {
        public string name;
        public string ID;
        public int roll_no;
        public Student()
        {
            Console.WriteLine("Default Constructor Invoked!");
            name = "John Ryno";
            ID = "MBA58955";
            roll_no = 859;
        }
    }

    public class Program
    {
        public static void Main()
        {
            Student s = new Student();
            Console.WriteLine(s.name + "\n" + s.ID + "\n" + s.roll_no);
        }
    }
}

Output:

Default Constructor Invoked!
John Ryno
MBA58955
859
```
In the code example above, we have specified the default constructor ourselves, but even if we don't do that, the compiler will automatically assign a default contructor to the class which is used for initialization of object of the class.

2. Parameterized Constructor
A constructor with at least one parameter is called as parameterized constructor.
```
using System;
namespace Studytonight
{
    public class Student
    {
        public string name;
        public string ID;
        public int roll_no;
        public Student(string n, string id, int rno)
        {
            name = n;
            ID = id;
            roll_no = rno;
            Console.WriteLine(name + "\n" + id + "\n" + roll_no);
        }
    }

    public class Program
    {
        public static void Main()
        {
            Student s1 = new Student("John Ryno", "MBA58955", 859);
            s1 = new Student("John Ryno", "MBA58955", 1577);
            Console.WriteLine();
        }
    }
}

Output:

John Ryno
MBA58955
859
John Ryno
MBA58955
1577
```
3. Copy Constructor
The copy constructor is used to create an object by copying all of its variables(attributes) from another object. This type of constructors are used for initializing a new instance from an existing one.
```
using System;
namespace Studytonight
{
    public class Student
    {
        public string name;
        public string ID;
        public int roll_no;
        public Student(string n, string id, int rno)
        {
            name = n;
            ID = id;
            roll_no = rno;
        }

        // Copy Constructor
        public Student(Student s)
        {
            name = s.name;
            ID = s.ID;
            roll_no = s.roll_no;
        }
    }

    public class Program
    {
        public static void Main()
        {
            Student s1 = new Student("John Ryno", "MBA58955", 859);
            Console.WriteLine("s1 is: " + s1.name + "\n" + s1.ID + "\n" + s1.roll_no);
            // Another student by copying student details
            Student s2 = new Student(s1);
            Console.WriteLine("s2 is: " + s2.name + "\n" + s2.ID + "\n" + s2.roll_no);
            s2.name = "Dyna Winta";
            s2.ID = "PHRMA96665";
            s2.roll_no = 122;
            Console.WriteLine("s2 is: " + s2.name + "\n" + s2.ID + "\n" + s2.roll_no);
        }
    }
}

Output:

s1 is: John Ryno
MBA58955
859
s2 is: John Ryno
MBA58955
859
s2 is: Dyna Winta
PHRMA96665
122
```

4. Private Constructor
A constructor that is preceded by a private access modifier is called a private constructor. It does not make it possible for other classes to inherit any data from this class (we can't instantiate the class if the constructor is private). We will cover more on this concept when we will cover the concept of inheritance.

Following are its characteristics:

Generally, private constructor is used in classes that contain static members only.

We can't create public and private constructors simultaneously in a class, both without parameters.

We can't instantiate the class with a private constructor.

If we want to create an object of a class with private constructor then, we need to have public constructor along with it
```
using System;
namespace Studytonight
{
    public class Student
    {
        public int roll_no;
        private Student()
        {
            Console.WriteLine("Private Constructor");
        }

        public Student(int rno)
        {
            roll_no = rno;
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            // Student s1 = new Student(); // it will generate an error because the constructor is inaccessible
            Student s1 = new Student(4559);
            Console.WriteLine(s1.roll_no);
        }
    }
}

Output:
4559
```
5. Static Constructor
This type of constructor will be invoked only once for all the instances of the class and it is invoked during the creation of the first instance of the class.

Following are its characteristics:

Static constructor neither accepts parameters nor access modifiers.

In a class, only one static constructor is allowed.

Static constructor will invoke automatically, whenever we create the first instance of a class.

It is used to initialize static fields of the class.
```
using System;
namespace Studytonight
{
    public class Student
    {
        static Student()
        {
            Console.WriteLine("Static Constructor");
        }

        public Student()
        {
            Console.WriteLine("Default Constructor");
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            Student s1 = new Student();
            Student s2 = new Student();
        }
    }
}

Output:

Static Constructor
Default Constructor
Default Constructor
```
If you observe the above example, we have created a static constructor as well as a default constructor. Here the static constructor will be invoked only once for the first instance of the class.

## Static Constructors and Inheritance
In general, when we create instance of a derived class, it internally calls the top most base class constructor and the call starts from there.
But when the derived class contains a static constructor, it is called first; even before the base class constructor is called.
If the base class also contains a static constructor, the derived class static constructor is followed by the base class static constructor and then the call goes to the base class constructor.
Example –
```
namespace DumpConsoleApp
{
    public class SomeBaseClass
    {
        static SomeBaseClass()
        {
            Console.WriteLine(
                "This is SomeBaseClass static constructor");
        }

        public SomeBaseClass()
        {
            Console.WriteLine(
                "This is SomeBaseClass constructor");
        }
    }

    public class SomeDerivedClass : SomeBaseClass
    {
        static SomeDerivedClass()
        {
            Console.WriteLine(
                "This is SomeDerivedClass static constructor");
        }

        public SomeDerivedClass()
        {
            Console.WriteLine(
                "This is SomeDerivedClass constructor");
        }
    }
}


#caller method#
SomeBaseClass b = new SomeDerivedClass();

#output:#
This is SomeDerivedClass static constructor
This is SomeBaseClass static constructor
This is SomeBaseClass constructor
This is SomeDerivedClass constructor

```

## SOLID Design Principles
1. Single Responsibility Principle (SRP)
The SRP states that a class should have only one reason to change, meaning it should have only one responsibility. This promotes modularization and makes the code easier to understand and maintain.

Key Idea: A class should do only one thing, and it should do it well.

Real-Time Example: Think of a chef who only focuses on cooking, not managing the restaurant or delivering food.

Practical coding example in C#:

Before applying for SRP:
```
public class Report
{
    public void GenerateReport() { }
    public void SaveToFile() { }
}
In this scenario, theReport class has two responsibilities: generating a report and saving it to a file. This violates the SRP.

After applying SRP:

public class Report
{
    public void GenerateReport() { }
}

public class ReportSaver
{
    public void SaveToFile() { }
}
```
Now, theReport class is responsible only for generating reports, while the ReportSaver class is responsible for saving reports. Each class has a single responsibility.

Explanation: According to SRP, one class should take one responsibility hence to overcome this problem we should write another class to save the report functionality. If you make any changes to theReport class will not affect the ReportSaver class.


2. Open/Closed Principle (OCP)
The Open/Closed Principle suggests that a class should be open for extension but closed for modification. This means you can add new features without altering existing code.

Key Idea: Once a class is written, it should be closed for modifications but open for extensions.

Real-Time Example: Your smartphone — you don’t open it up to add features; you just download apps to extend its capabilities.

Practical coding example in C#:

Before applying for OCP:
```
public class Rectangle
{
    public double Width { get; set; }
    public double Height { get; set; }
}

public class AreaCalculator
{
    public double CalculateArea(Rectangle rectangle)
    {
        return rectangle.Width * rectangle.Height;
    }
}
This design may become problematic when adding new shapes. Modifying the AreaCalculator for each new shape violates the OCP.

After applying for OCP:

public interface IShape
{
    double CalculateArea();
}

public class Rectangle : IShape
{
    // implementation
}

public class Circle : IShape
{
    // implementation
}
```
By introducing an interface (IShape), new shapes like Circle can be added without modifying existing code, adhering to the OCP.

Explanation: According to OCP, the class should be open for extension but closed for modification. So, When you introduce a new shape, then just implement it from the interface IShape. So IShapeis open for extension but closed for further modification.

3. Liskov Substitution Principle (LSP)
The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

Key Idea: You should be able to use any subclass where you use its parent class.

Real-Time Example: You have a remote control that works for all types of TVs, regardless of the brand.

Practical coding example in C#:
```
Before applying for LSP:

public class Bird
{
    public virtual void Fly() { /* implementation */ }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException("Penguins can't fly!");
    }
}
Here, the Penguin class violates the LSP by throwing an exception for the Fly method.

After applying for LSP:

public interface IFlyable
{
    void Fly();
}

public class Bird : IFlyable
{
    public void Fly()
    {
        // implementation specific to Bird
    }
}

public class Penguin : IFlyable
{
    public void Fly()
    {
        // implementation specific to Penguins
        throw new NotImplementedException("Penguins can't fly!");
    }
}
```
By introducing the IFlyable interface, both Bird and Penguin adhere to the Liskov Substitution Principle.

Explanation: According to LSP, a derived class should not break the base class’s type definition and behavior which means objects of a base class shall be replaceable with objects of its derived classes without breaking the application. This needs the objects of derived classes to behave in the same way as the objects of your base class.

4. Interface Segregation Principle (ISP)
The Interface Segregation Principle states that a class should not be forced to implement interfaces it does not use. This principle encourages the creation of small, client-specific interfaces.

Key Idea: A class should not be forced to implement interfaces it doesn’t use.

Real-Time Example: You sign up for a music streaming service and only choose the genres you like, not all available genres.

Practical coding example in C#:

Before applying for ISP:
```
public interface IWorker
{
    void Work();
    void Eat();
}

public class Manager : IWorker
{
    // implementation
}

public class Robot : IWorker
{
    // implementation
}
The Robot class is forced to implement the Eat method, violating ISP.

After applying for ISP:

public interface IWorkable
{
    void Work();
}

public interface IEatable
{
    void Eat();
}

public class Manager : IWorkable, IEatable
{
    // implementation
}

public class Robot : IWorkable
{
    // implementation
}
```
By splitting the IWorker interface into smaller interfaces (IWorkable and IEatable), classes can implement only what they need, adhering to ISP.

Explanation: According to LSP, any client should not be forced to use an interface that is irrelevant to it. In other words, clients should not be forced to depend on methods that they do not use.

5. Dependency Inversion Principle (DIP)
The Dependency Inversion Principle suggests that high-level modules should not depend on low-level modules, but both should depend on abstractions. Additionally, abstractions should not depend on details; details should depend on abstractions.

Key Idea: High-level modules should not depend on low-level modules; both should depend on abstractions.

Real-Time Example: Building a LEGO tower — the bricks (high and low-level modules) connect through smaller bricks (abstractions).

Practical coding example in C#:

Before applying DIP:
```
public class LightBulb
{
    public void TurnOn() { /* implementation */ }
    public void TurnOff() { /* implementation */ }
}

public class Switch
{
    private LightBulb bulb;

    public Switch(LightBulb bulb)
    {
        this.bulb = bulb;
    }

    public void Toggle()
    {
        if (bulb.IsOn)
            bulb.TurnOff();
        else
            bulb.TurnOn();
    }
}
```
The Switch class directly depends on the concrete LightBulb class, violating DIP.

After applying DIP:
```
public interface ISwitchable
{
    void TurnOn();
    void TurnOff();
}

public class LightBulb : ISwitchable
{
    // implementation
}

public class Switch
{
    private ISwitchable device;

    public Switch(ISwitchable device)
    {
        this.device = device;
    }

    public void Toggle()
    {
        if (device.IsOn)
            device.TurnOff();
        else
            device.TurnOn();
    }
}
```
By introducing an interface (ISwitchable), the Switch class now depends on an abstraction, adhering to the Dependency Inversion Principle.

Explanation: According to DIP, do not write any tightly coupled code because that is a nightmare to maintain when the application is growing bigger and bigger. If a class depends on another class, then we need to change one class if something changes in that dependent class. We should always try to write loosely coupled classes.
