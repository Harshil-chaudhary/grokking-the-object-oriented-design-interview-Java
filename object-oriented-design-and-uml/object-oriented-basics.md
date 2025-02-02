<h1 align="center">Object Oriented Basics</h1>

Object-oriented programming (OOP) is a style of programming that focuses on using objects to design and build applications. Contrary to procedure-oriented programming where programs are designed as blocks of statements to manipulate data, OOP organizes the program to combine data and functionality and wrap it inside something called an “Object”.

If you have never used an object-oriented programming language before, you will need to learn a few basic concepts before you can begin writing any code. This chapter will introduce some basic concepts of OOP:

* **Objects:** Objects represent a real-world entity and the basic building block of OOP. For example, an Online Shopping System will have objects such as shopping cart, customer, product item, etc.

* **Class:** Class is the prototype or blueprint of an object. It is a template definition of the attributes and methods of an object. For example, in the Online Shopping System, the Customer object will have attributes like shipping address, credit card, etc., and methods for placing an order, canceling an order, etc.

**A Simple Code Snippet of Class and Object**

**Class Code Snippet:**
Python

```python
class ShoppingCart(object):

    def __init__(self):
      self.total = 0
      self.items = {}

    def add_item(self, item_name, quantity, price):
        self.total += (quantity * price)
        self.items.update({item_name : quantity})


    def remove_item(self, item_name, quantity, price):
        self.total -= (quantity * price)
        if quantity > self.items[item_name]:
          del self.items[item_name]
        self.items[item_name] -= quantity


    def checkout(self, cash_paid):
        balance = 0
        if cash_paid < self.total:
          return "You paid {} but cart amount is {}".format(cash_paid, self.total)
        balance = cash_paid - self.total
        return "Exchange amount: {}".format(balance)
```
Java
```java
import java.util.HashMap;
import java.util.Map;

public class ShoppingCart {
    private double total;
    private Map<String, Integer> items;

    public ShoppingCart() {
        this.total = 0.0;
        this.items = new HashMap<>();
    }

    public void addItem(String itemName, int quantity, double price) {
        this.total += (quantity * price);
        items.put(itemName, items.getOrDefault(itemName, 0) + quantity);
    }

    public void removeItem(String itemName, int quantity, double price) {
        if (items.containsKey(itemName)) {
            this.total -= (quantity * price);
            int remainingQuantity = items.get(itemName) - quantity;
            if (remainingQuantity <= 0) {
                items.remove(itemName);
            } else {
                items.put(itemName, remainingQuantity);
            }
        }
    }

    public String checkout(double cashPaid) {
        if (cashPaid < total) {
            return "You paid " + cashPaid + " but cart amount is " + total;
        }
        double balance = cashPaid - total;
        return "Exchange amount: " + balance;
    }

    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        cart.addItem("Apple", 2, 1.50);
        cart.addItem("Banana", 1, 0.75);
        System.out.println(cart.checkout(5));  // Example checkout
    }
}

```

**Object and it's Uses Code Snippet:**
Python
```python
# Driver code
cart = ShoppingCart()

cart.add_item('A', 10, 50)
cart.add_item('B', 5, 20)

cart.remove_item('B', 1, 20)

cart_res = cart.checkout(600)

print('Total cart amount:', cart.total)
print('Cart items:', cart.items)

print(cart_res)
```
Java
```java
public class ShoppingCartDriver {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        cart.addItem("A", 10, 50);
        cart.addItem("B", 5, 20);

        cart.removeItem("B", 1, 20);

        String cartRes = cart.checkout(600);

        System.out.println("Total cart amount: " + cart.getTotal());
        System.out.println("Cart items: " + cart.getItems());
        System.out.println(cartRes);
    }
}

```

**Response:**
```
Total cart amount: 580
Cart items: {'B': 4, 'A': 10}
Exchange amount: 20
``` 

<p align="center">
    <img src="/media-files/oop-principles.svg" alt="OOP Principles">
</p>

The four principles of object-oriented programming are encapsulation, abstraction, inheritance, and polymorphism.

* **Encapsulation:** Encapsulation is the mechanism of binding the data together and hiding it from the outside world. Encapsulation is achieved when each object keeps its state private so that other objects don’t have direct access to its state. Instead, they can access this state only through a set of public functions.

**Encapsulation Code Snippet:**

```python
class Product:

    def __init__(self):
        self.__maxprice = 900

    def sell(self):
        print("Selling Price: {}".format(self.__maxprice))

    def set_max_price(self, price):
        self.__maxprice = price

product = Product()
product.sell()

# change the price
product.__maxprice = 1000
product.sell()

# using setter function
product.set_max_price(1000)
product.sell()
```
Java
```java
class Product {

    private int maxPrice = 900;

    public void sell() {
        System.out.println("Selling Price: " + maxPrice);
    }

    public void setMaxPrice(int price) {
        maxPrice = price;
    }

    public static void main(String[] args) {
        Product product = new Product();
        product.sell();

        // Attempt to change the price directly (won't work in Java due to private access modifier)
        // product.maxPrice = 1000; // This would result in a compile-time error

        // Using setter function
        product.setMaxPrice(1000);
        product.sell();
    }
}

```


**Response:**
```
Selling Price: 900
Selling Price: 900
Selling Price: 1000
```

* **Abstraction:** Abstraction can be thought of as the natural extension of encapsulation. It means hiding all but the relevant data about an object in order to reduce the complexity of the system. In a large system, objects talk to each other, which makes it difficult to maintain a large code base; abstraction helps by hiding internal implementation details of objects and only revealing operations that are relevant to other objects.

**Abstraction Code Snippet:**

```python
from abc import ABC, abstractmethod

class Parent(ABC):
  def common(self):
    print('In common method of Parent')

  @abstractmethod
  def vary(self):
    pass

class Child1(Parent):
  def vary(self):
    print('In vary method of Child1')

class Child2(Parent):
  def vary(self):
    print('In vary method of Child2')

# object of Child1 class
child1 = Child1()
child1.common()
child1.vary()

# object of Child2 class
child2 = Child2()
child2.common()
child2.vary()
```
Java
```java
abstract class Parent {
    // Common method
    public void common() {
        System.out.println("In common method of Parent");
    }

    // Abstract method
    public abstract void vary();
}

class Child1 extends Parent {
    @Override
    public void vary() {
        System.out.println("In vary method of Child1");
    }
}

class Child2 extends Parent {
    @Override
    public void vary() {
        System.out.println("In vary method of Child2");
    }
}

public class Main {
    public static void main(String[] args) {
        // Object of Child1 class
        Child1 child1 = new Child1();
        child1.common();
        child1.vary();

        // Object of Child2 class
        Child2 child2 = new Child2();
        child2.common();
        child2.vary();
    }
}

```


**Response:**
```
In common method of Parent
In vary method of Child1
In common method of Parent
In vary method of Child2
```

* **Inheritance:** Inheritance is the mechanism of creating new classes from existing ones.

**Inheritance Code Snippet:**

```python
class Person(object): 

    def __init__(self, name):
        self.name = name

    def get_name(self):
        return self.name

    def is_employee(self):
        return False
   

class Employee(Person):

    def is_employee(self): 
        return True
   
# Driver code
emp = Person("Person 1")
print("{} is employee: {}".format(emp.get_name(), emp.is_employee()))

emp = Employee("Employee 1")
print("{} is employee: {}".format(emp.get_name(), emp.is_employee()))
```
Java
```java
class Person {

    private String name;

    // Constructor
    public Person(String name) {
        this.name = name;
    }

    // Getter method
    public String getName() {
        return name;
    }

    // Method to check if the person is an employee
    public boolean isEmployee() {
        return false;
    }
}

class Employee extends Person {

    // Constructor
    public Employee(String name) {
        super(name);
    }

    // Overriding method to indicate if the person is an employee
    @Override
    public boolean isEmployee() {
        return true;
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating a Person object
        Person person = new Person("Person 1");
        System.out.println(person.getName() + " is employee: " + person.isEmployee());

        // Creating an Employee object
        Employee employee = new Employee("Employee 1");
        System.out.println(employee.getName() + " is employee: " + employee.isEmployee());
    }
}

```


**Response:**
```
Person 1 is employee: False
Employee 1 is employee: True
```

* **Polymorphism:** Polymorphism (from Greek, meaning “many forms”) is the ability of an object to take different forms and thus, depending upon the context, to respond to the same message in different ways. Take the example of a chess game; a chess piece can take many forms, like bishop, castle, or knight and all these pieces will respond differently to the ‘move’ message.

**Polymorphism Code Snippet:**

```python
class Bishops:

    def move(self):
        print("Bishops can move diagonally")

class Knights:

    def move(self):
        print("Knights can move two squares vertically and one square horizontally, or two squares horizontally and one square vertically")

# common interface
def move_test(chess_piece):
    chess_piece.move()
# Driver code

#instantiate objects
bishop = Bishops()
knight = Knights()

# passing the object
move_test(bishop)
move_test(knight)
```
```java
// Interface for chess pieces
interface ChessPiece {
    void move();
}

// Bishops class implementing ChessPiece interface
class Bishops implements ChessPiece {
    @Override
    public void move() {
        System.out.println("Bishops can move diagonally");
    }
}

// Knights class implementing ChessPiece interface
class Knights implements ChessPiece {
    @Override
    public void move() {
        System.out.println("Knights can move two squares vertically and one square horizontally, or two squares horizontally and one square vertically");
    }
}

// Common method to test move
public class Main {
    public static void moveTest(ChessPiece chessPiece) {
        chessPiece.move();
    }

    public static void main(String[] args) {
        // Instantiate objects
        ChessPiece bishop = new Bishops();
        ChessPiece knight = new Knights();

        // Passing the object to the moveTest method
        moveTest(bishop);
        moveTest(knight);
    }
}

```


**Response:**
```
Bishops can move diagonally
Knights can move two squares vertically and one square horizontally, or two squares horizontally and one square vertically
```
