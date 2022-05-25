## Access Modifiers
- public - Anyone can modify/see it
- internal - Must be in same project
- protected - Only classes that inherit from this
- private - only this class

## Fields
Fields keep internal state (normally). Only the current instance can access the value

## Static field
all the instances share the value in the static field and can access it

## Static Method - can be called from class `Car.MyStaticMethod()`. Can only access static fields
```
    class Counter
    {
        private static int _count = 0;
        private int _no = 0;

        public Counter()
        {
            _count = _count + 1;
            _no = _count;
        }

        // can access both static field and non static fields
        public string GetInstanceNo()
        {
            return $"I am no: {_no} out of {_count}.";
        }

        // static method. Cannot access non static fields
        public static string GetInstanceNoStatic()
        {
            // cannot access  _no
            return $"{_count} instances have been created";
        }
    }
```
## Properties
Properties - Like fields but allow you to control how the variable is changed. 
We also have Properties with a backing field
```cs
    class Program
    {
        static void Main(string[] args)
        {
            var car = new Car("Toyata");
            var ferrai = new Car("Ferrai");

            Console.WriteLine(car.Type);
            // can't do: car.Type = "Kia";
            Console.WriteLine($"The car has {car.GetNumberOfWheels()}");

            Console.WriteLine(car.IsExpensiveCar());
            Console.WriteLine(ferrai.IsExpensiveCar());

            var first = new Counter();
            var second = new Counter();
            first = new Counter();
            first = new Counter();

            Console.WriteLine("first " + first.GetInstanceNo());
            Console.WriteLine("second " + second.GetInstanceNo());

            Car.IsExpensiveCarStatic("Kia");
        }
    }
    ```
    ```cs
    public class Vehicle
    {
        protected int _wheels = 0;
    }

    public class Car:Vehicle
    {
        // fields naming convention is _camelCase
        // [Access Modifier] [static] [type] [name] [= ...]
        private string _make;

        // Properties naming convention is CamelCase
        // [Access Modifier] [type] [name] {get; set;}
        public string Type { get; private set; }

        // Property with a backing field
        public string Make
        {
            get { return _make; }
            private set
            {
                if (!value.Contains(" "))
                {
                    _make = value;
                }
            }
        }

        public Car(string make)
        {
            _wheels = 4;
            _make = make;
            Type = make;
        }

        public int GetNumberOfWheels()
        {
            return _wheels;
        }

        // Static method. Can't access _make as it is not a static field
        public static string IsExpensiveCarStatic(string make)
        {
            if (make == "Ferrai")
            {
                return "This is an Expensive car";
            }

            return "CheapCar";
        }

        public string IsExpensiveCar()
        {
            var toReturn = "This car is not a toyata, The best car in the world";
            if (_make == "Ferrai")
            {
                toReturn = "This is an Expensive car";
            }
            else if (_make == "Toyata")
            {
                toReturn = "The best car in the world";
            }
            else if (_make == "BMW")
            {
                toReturn = "BMW's are shit";
            }

            return toReturn;
        }
    }
    ```
    
