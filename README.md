# Java8 New main features
--------------------------
		1. Lambda Expressions
		2. Functional Interfaces
		3. Default Methods
	Predefined Functional Interfaces
		4. Predicates
		5. Functions
			Supplier
			Consumer
		6. Double Colon Operator (Constructor and Method references)
		7. Stream API
		8. Date and Time API(Joda Time API)
		9. Etc..
			

default method
--------------
	1. It is available from Java 8 only and it is available in FunctionalInterface.
	2. default method can have implementation but the classes implemented the interface no need to implement this method. If they want they can override.
	3. It can't override the methods in Object class(Eg : toString(), hashCode()). It is not needed becaues Object class methods are already available in all java classes.
	4. default keyword is not a modifer. It will be used in 2 places in Java. Switch statements and default method in the interfaces.
	5. public keyword infront of default keyword is perfectly valid because any method in Interface is public by default. - Eg : public default void toPrint() {s.o.p ("print");}
	6. Default method can be called by using the functional interface reference which was aquired from lambda expressions eg:
		TestInterface i = name-> System.out.println("My Name is:"+name);
			i.print("Arun"); // this is a default method in TestInterface 
	
	
Interface methods in Java 8
---------------------------
	1. public and abstract
	2. default
	3. static
	
	
	
	
Functional Interface
--------------------





Lambda expression examples
--------------------------
1.
	@FunctionalInterface
	public interface TestInterface {
		public abstract int multiply(int a, int b) ;
	}
	
	public class TestClass {
		public static void main(String[] args) {
			TestInterface i = (a,b)-> { 
				int c = a + 10;
				return c*b;};
			System.out.println(i.multiply(10, 20));
		}
	}
2. 
	public class TestClass {
		public static void main(String[] args) {
			TestInterface i = (a,b)-> a*b;
			System.out.println(i.multiply(10, 20));
		}
	}
	
3. 
	public interface TestInterface {
		public abstract Employee multiply(int empId, String empName, Date joiningDate);
	}
	
	class Employee {
		private int empId;
		private String empName;
		private Date joiningDate;
	}
	
	public class TestClass {
		public static void main(String[] args) {
			TestInterface i = (empId, empName, joiningDate)-> {
				return new Employee(empId, empName, joiningDate);
			};
			System.out.println(i.multiply(10, "John", new Date()));
		}
	}
	
4. 
	public interface TestInterface {
		public abstract void print(String name) ;
	}
	
	public class TestClass {
		public static void main(String[] args) {
			TestInterface i = name-> System.out.println("My Name is:"+name);
			i.print("Arun");
		}
	}
	

Multipe Inheritance
-------------------

	
Instance methods & Static methods
----------------------------------
Instance methods:
	Always talks about Object

Static methods:
	Never talks about the Object
	Static metholds are mostly used for General utility methods 
		Static methods in Interface
		---------------------------
		1. Static methods in interface are to define general utility methods which doesn't require of instance variables.
		2. Interface static methods by default not available to the implementation classes. Static methods in Interface are not inherited to the child classes so it won't be called by using child class name or with any class instance variables. It will be called by using only interface name Eg :
			interface Interf {
				public static void add(int x, int y) {
						s.o.p("Print my message:"+ x+y)
					}
			}
			class Test {
				public static void main(String[] args) {
						Test.add(10,20); // Assume class Test implements Interf - Invalid becase child class can't access the parent interface's static methods
						
						Test t = new Test(); // Invalid
						t.add(10,20);
						
						Interf.add(10,20); // Only Valid -  compulsary to use only Interface name.
					}
			}
		3. Child class can have the same static method as in the interface, but it is not called overriding. It acts as a new method in the class.
		4. Child class static method can override the parent class static method but the scope of access modifier should not be reduced(public to private).
		5. If a class has static method, it can be accessible using class name and with the instance variable reference.
		6. Till 1.7 version
			public static final variables are allowed
			public and abstract methods are available
		7. In 1.8 version
			In addition to till 1.7 version features
				default methods
				public static methods are available
		8. In 1.9 version
				private instance methods
				private static methods
					Above 2 methods are for code resusability purpose, some commom codes can be placed in this method and other default/instance or static methods can use it by call it from the same interface)
					
Collections and Streams
-----------------------
	
	
