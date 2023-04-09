
### Single Responsiblity Principle

A class should have only one reason to change ie only one responsibility.

```java
public class Marker {
	private String color;
	private String price;

	public Marker(String color, String price){
		this.color = color;
		this.price = price;
	}

	// getters and settters
} 
```

```java
public class Invoice{
	private Marker marker;
	private int quantity;

	public Invoice(Marker marker, int quantity){
		this.marker = marker;
		this.quantity = quantity;
	}

	public double priceCalculation(){
		return (this.marker.price * this.quantity);
	}

	public void saveToDB(){
		// insert to db
	}

	public void printInvoice(){
		// print invoice	
	}
}
```

Here Invoice class has more than one method. If in future price calculation changes then we have to modify Invoice class. Similarly changes in saveToDb() and printInvoice() change the blueprint of class Invoice. Since there are more than one reason to change, class Invoice does not follow `S - principle`.

Solution :

Create a separate class for saveToDB() and printInvoice().

```java
public class InvoiceDao{
	private Invoice invoice;

	//constructor

	public void saveToDB(){
		// save to db
	}
}

public class InvoicePrinter{
	private Invoice invoice;
	// constructor
	public void printInvoice(){
		// print
	}
}
```

Code is now easy to maintain and understand.



### Open / Close Principle

Open for extension but closed for modification.

```java
public class InvoiceDao{
	private Invoice invoice;

	//constructor

	public void saveToDB(){
		// save to db
	}
}
```

Let's say I want to add new functionality to current class. So if we modify the class, then it is prone to bugs, since new functionality might break the alredy tested class. Hence instead of modifying already tested class, extend it.

```java
interface InvoiceDao{
	public void save();
}

public class DBInvoiceDao implements InvoiceDao{

	public void save(){
		// save invoice to db
	}
}

public class FileInvoiceDao implements InvoiceDao {
	public void save(){
		// save to file
	}
}
```







### Liskov Substitution Principle

If class B is a subclass of class A, then we should be able to replace object of A with object of B without breaking the behaviour of the program.
Basically, subclass must extend all the capabilities of super class and must not narrow it down.

```java
interface Bike {
	public void turnOnEngine();
	public void accelerate();
}

class MotorCycle implements Bike {
	boolean isEngineOn;
	int speed;
	public void turnOnEngine(){
		// turn on the engine
	}
	public void accelerate(){
		// increase the speed
	}
}

class Bicycle implements Bike {
	int speed;
	public void turnOnEngine(){
		thow exception;
	} // narrowing down the capability of parent class

	public void accelerate(){
		// increase speed
	}

}
```

Here object of Bicycle cannot be replaced with object of Bike because it is narrowing the turnOnEngine functionality and throwing exception.




### Interface Segmentation Principle

Interface should be such that the client should not implement unnecessary functions.

```java
interface RestaurantEmp {
	void washDishesh();
	void cookFood();
	void serveCustomer();
}

class Waiter implements RestaurantEmp {
	void washDishesh(){
		// not my job
	}
	void cookFood(){
		// not my job
	}
	void serveCustomer(){
		System.out.println("serving customer")
	}
}
```

Here Waiter class had to implement unnecessary functions like washDishesh() and cookFood().
Hence seggregating the interface into small interfaces.

```java
interface WaiterInterface {
	void serveCustomer();
	void takeOrder();
}

interface ChefInterface {
	void cookFood();
	void decideTodaysSpecial();
}
```

Dividing large interface so that implementing class doesn't have to implement unnecessary methods.


### Dependency Inversion Principle

Class should depend on interface rather than concrete classes. Interface should depend on Interface.

If class A is parent class of B and class B is parent of class C. Here slight change in A might affect the behaviour of class C. Because the these classes are tightly coupled.
To avoid such situation, let the class implement from interface and also make child interface dependend on parent interface.

```java
interface A {

}

Class A implements A {

}

Interface B extends B {

}

class B implements B {

}

Class C implements B {

}
```

Check the `Dependency Inversion Principle With Diagram.canvas`

### Advantages of SOLID Principles

Help us to write better code.
+ Avoid duplicate code
+ easy to maintain
+ easy to understand
+ flexible software
+ reduce complexity







