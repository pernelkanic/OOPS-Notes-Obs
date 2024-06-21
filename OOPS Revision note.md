# Concepts to mainly cover
- Static
- Final
- Inheritance
- Polymorphism
- abstraction
- Encapsulation
- Abstract Methods
- Interfaces


## Static 
 Static is a keyword in java used to represent that the methods or the members of a class is beyond the concept of objects , it is shared by all the objects . for example if i create a class and declare the methods of the class static , if i create a object for that class and try to access the methods or the variables , every object will give me the same result

- Anything that involves the use of object cannot be used here
```
public class staticmain {
	public static void main(String[] args) {
		staticexample st = new staticexample(2,4,5);
		st.printPop();
		staticexample st1 = new staticexample(4,5,6);
		st1.printPop();
	}
}
 class staticexample{
	static int pop  = 10;
	int age ;
	int name;
	int money;
	
	staticexample(int age , int name , int money ){
		this.age = age;
		this.name = name;
		this.money = money;
		staticexample.pop+=1; // we have to use the class name to access the static stuff here it is the convention.
	}
	public void printPop() {
		System.out.println(pop);
		
	}
	
}

```
- you cannot reference non static stuff inside static methods without creating its own object but if i use a non static stuff inside non static object , anyways in main the object to that parent non static should be created so , it wouldnt be a issue to create a object for the child as well.
- ```this``` keyword cannot be used inside static stuff as this depends on objects , static does nt depend on objects so , we cannot use this inside static.
- there is a initialisation pattern for the static stuff , for example take two var.

``` 
static int a  = 5;
static int b = 6;
static{ // use this to perform computation on static stuff
	b = a*b;
	System.out.println("inside static block");
}
```

## Singleton classes

- This is a type of design pattern where if i try to create more than one object for a specific singleton implemented class , the same object created for the first time is referenced to the newly created object.
```
public class Singleton {
	public static void main(String[] args) {
		Singletonexample obj1 = new Singletonexample();
		Singletonexample obj2 = new Singletonexample(); //all these 3 objects will be pointed to the same instance which was created for the first time in the line 5;
		Singletonexample obj3 = new Singletonexample();
		
	}
}
class Singletonexample{
	Singletonexample(){
		
	}
	
	
	private static Singletonexample instance;
	public static Singletonexample getInstance() {
		if(instance == null) {
			instance = new Singletonexample();
			
		}
		return instance;
		
	}
}

```
---
## Inner Classes
- the main point that needed to be understood is we can declare classes inside classes and they depend on the parent class objects that need to be created , so they give an error 
- for resolving that we can put ```static innerclassname``` to make it dependent on the parent class only and not its objects and also main point about making the inner class static doesnt mean  we cannot create objects of it , we can create objects of the innerclass but that class is dependent only on the parent class only and not parent class objects.

That is all i can say abt innerclasses.
- **if u dont get it, leave it** .
---

# Inheritance
- we know what inheritance is , it is through which we can access all the members of the inherited parent classes.
- we use extends keyword for inheritance.

	## types of inheritance:
	 - single inheritance
	 - multiple inheritance through interfaces
	 - Hierarchial inheritance - where A can extend parent , B can extends parent , C can also extend parent.
	 - Hybrid inheritance

	### why multiple inheritance is not supported
	- mainly because lets take a class a and class b and we have a child class C which extends both a and b , such that a and b both have  a method called as getName() , when use that c object to call the getName() function , the compiler panicks on which instance of the getName name to call , A or B , so multiple inheritance is not supported.
	## Super Keyword
	- This keyword is mainly used to call the parent class constructor.
	- Nothing else, and we can also access the methods of the parent class using super just like this is for the current class
	``` 
		// This is a example of single/Single Level inheritance.
		class A extends B{
			int a = 5;
			A(int val){
				super(val); //inside the constructor A i can initialize the members of A and B as well using super
			}
			public void sayA() {
				System.out.println("Hey im A");
			}
			public void saya() {
				System.out.println(a);
			}
			
			
		}
		class B{
			int b ;
			
			B(int b){
				this.b = b;
			}
			public void sayB() {
				System.out.println("Hey im B");
			}
			public void sayb() {
				System.out.println(b);
			}
		}
	```
	## Hybrid Inheritance:
		![[hybrid.PNG]]

# PolyMorphism
- The very important concept of oops is polymorphism
- The methodology of expressing the same thing in multiple ways .
- There are two types for this:
	- Compile Time(static) polymorphism
	- RunTime(Dynamic) polymorphism
- any language in deficit of this concept is object based and not object oriented.

	## Static polymorphism
	This is called as static polymorphism as the resolving the which method to run is decided at compile time rather than at run time.
		
	- Let's say There is a method called greet() in class A and there is another method with the same name but with different paramter , accepting a name . these two are treated as diff methods as even though the name is same the return type , number of parameters differs it.
	- This is done through method overloading- i.e resolving  which method to run is known at compile time.
	- let us see a example.
	```
	public class Polymorphism {
			public static void main(String[] args) {
				Polyexamplestatic obj = new Polyexamplestatic();
				obj.greet();//prints say hello
				obj.greet("venkat"); // prints say helo venkat
				
			}
		}
	class Polyexamplestatic{
		public void greet() {// this do not have a arguement 
			System.out.println("Say hello");
		}
		public void greet(String name) {//this has a arguement 
			System.out.println("Say helo" + name);
		}
		}
	```
	## RunTime Polymorphism
	- This is called runtime , as which object to run is resolved at runtime rather than at compile time.
	- it done using method overriding, whereby if a class C inherits class A , then , if i create a greet method in C which is in A as well , then child class method will run due to overriding.
	- for example 

		**```Parent obj = new Child()```**
	- here Parent is the reference that tells us what all we can access , in this case we can access all the members of the parent class, and which one of it to access is said by the child reference on the right.

	
	```
	public class Polymorphism {
		public static void main(String[] args) {
			shapes obj = new Polyexampleruntime();
			obj.sayThis(); //hey im child of shapes :O/P
			
		}
	}
	//child class extending parent class
	class Polyexampleruntime extends shapes{
		@Override	
		public void sayThis() {
				System.out.println("hey im child of shapes");
			}
	}
	//parent class
	class shapes{
		
		public void sayThis() {
			System.out.println("hey im shapes");
		}
	}
	```
	- ```Parent obj // reference variable = new Child() //type of the object```
	 here the Parent is the reference variable telling us what all from the parent class we have access to and we use the child() to tell java we need the method which is in the parent class but overridden in the child class like in the above code.
	 - **Upcasting** : which version of the method to run is determined by the right hand side of the object initialization.
	 - **Dynamic Method Dispatch**:  Process of resolving the which version of the method to run is done at run time rather than at compile time , it is called dynamic method dispatch.
	also called **Late Binding**.
--- 
# Final Keyword
- To say shortly , anything that is declared final cannot be changed.
- **Classes** declared Final Cannot be inherited.
- **In Polymorphism** , if we declare a method final it cannot be overridden.
- **Early Binding**: If a method is declared final , the compiler can consider this method as final , as it cannot be overridden and resolves it at compile time , hence the name.
- **LateBinding**: If resolving is done at run time.

## Can we Override Static Methods:
 - The answer is **NO** 
 - Why? Static methods does nt depend on objects , The method in the parent class will run no matter from which object it is called , as it doesnt depend on objects , so makes no sense to override static methods.
 - ___To say simply, overriding depends on objects , static doesnt depend on objects , so static methods cannot be overridden.___ 

---
# Encapsulation And Abstraction
 - To explain this let us take a simple analogy ,if i have to drive a car all i need is a key , i dont need to know abt what the engine is , what horsepower it has , all i need is the key.
 - likewise , in **Abstraction** we dont care abt what that class contains ,all i need are the  methods to manipulate my data using this class. for example , System.out.println() where by we dont care how the println() fn is implemented , all i need is the way to use like ```println()``` that is abstraction , hiding away unnecessary details and showing only methods to manipulate it.
 - Encapsulation is basically wrapping up all the implementation level stuff. that is it . Both abstraction and encapsulation may look the same , but they are interrelated in way encapsulation is used to wrap up the big pile of code inside a class and abstraction is a way to show the clients how to use that wrapped up class methods to manipulate their data.
---
# Abstract Classes
- The classes which are declared with the abstract keyword are called abstract classes , 
- In the abstract Classes we declare the function alone and the body can be implemented in the children class inheriting the abstract class.
- if any of the fields inside the class is declared abstract , then the class has to be abstract.
- we cannot create objects of the abstract classes, why due to security reasons , whereby if a abstract method which is not implemented is called using that object,what output would java provide , so objects of abstract classes cannot be created.
- Let us take an example to see how these work

  ```
	public class AbstactClassesExample {

		public static void main(String[] args) {
			parent ch = new child(2);//abstract parent class can be referenced , but the one in the child class (right side) will be called.
			ch.identify(); // op - Hey im son
			

		}

	}
	abstract class parent{
		final int val;
		parent(int val ){
			this.val = val;
		}
		static void greet() { //works
			System.out.println("hello from a static methods"); 
		}
		abstract void identify();
	}

	class child extends parent{
		child(int val){
			super(val);
		}
		@Override
		void identify() {
			System.out.println("Hey im son");
			
		}
		
	}

  ```
 
 ## Can we use abstract static methods
  - NO ,  because abstract methods needs to be overridden but static methods cannot be overridden so we can't use abstact static methods , 
  - but we can create normal static methods inside abstract classes
---
# Interfaces
- similar to abstract classes , we have to do the fn declaration here , but body of the function cannot be implemented in the interface.

- We can do Multiple Inheritance here , why ? , we can implement any number of interfaces we want and the body of the functions in the interfaces has to be implemented in the child class only, so even if 2 interfaces has the same method , the body for it is implemented in the child.

- Even two dissimilar interfaces can be implemented , having no connection to each other , there is no heirarchy in the world of interfaces.

- In a interface we can extend another interface as well.

- The access modifier of the implemented method must be equal or better than the one declared in interface , if the interface has  a method protected , then the one implementing has to have protected or public.

- By Default, In the interfaces all the methods and variables are declared static and final.

- if we have a situation where we have to implement a method body in the interface , we use ```default``` keyword before the function to write the function body in the interface.
- There is concept of Nested Interfaces, which almost is same as nested class and nested can be protected , private or public , but the top level interface must be public.
- Let us take a example:
```
//Interface
public interface exampleInterface {
	 void greet();
	void saymyName();
	
	int val  =5 ;
}

//implemented class

public class InterfaceMain implements exampleInterface {

	public static void main(String[] args) {
		InterfaceMain main = new InterfaceMain();
		main.greet();
		main.saymyName();

	}

	@Override
	public void greet() {
		System.out.println("helo from interface class");
		
	}

	@Override
	public void saymyName() {
		System.out.println("Now Say my name");
		
	}

}

```
