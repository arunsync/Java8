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
Lambda expression
-----------------
Lambda expression: 
	1. To Enable functional programming in Java (Eg : a=f(), f(f1);  For function, you can pass another function as a arguement).
	2. It is a anonymous(nameless) function. Not having name, return type, modifiers
	Having this we can write simpe code
	
Programming languages which use Lambda expressions today
	1. Python
	2. Ruby
	3. Javascript
	4. C#
	6. C, C++
	5. Etc...

Example 1:

	public void m1() {
			System.out.println("Hello");
		}

	Remove method name, return type and modifier.. only below stmts will be there
		() {
			System.out.println("Hello");
		}
	Lambda expression for the above method with arrow symbol:
		() -> { System.out.println("Hello"); }

		if there is only one stmt, curly braces are not required
	Final lambda expression
		()-> System.out.println("Hello");

Example 2:

	public void m1(int a, int b) {
			System.out.println(a+b);
		}
	Lambda expression for the above method is:
		(int a, int b) -> System.out.println(a+b);
	
	Based on the cotext,compiler can able to guess the parameter data type
		(a,b) -> System.out.println(a+b);
Example 3:
	
	public int square(int n) {
			return n * n;
		}
	Lambda expression for the above method is:
		(n) -> return n * n;
	
	if only one arg is there, paranthesis are optional. If there are more than 1 args, paranthesis are required.
		n -> return n * n;
	
	compiler is going to guess we are returning n * n, so return stmt is not needed
		n -> n * n;

Conclusions:
	1. Any number of arguments (0, 1, 2 ...)
	2. If only one arg lambda expression is there, paranthesis are optional
	3. (a,b)->sop(a+b); Compiler will guess the type of the arguements
	4. If multipe lines are there, curly braces are required
		(a,b)->{ sop(a+b);
			sop(a-b);
			sop(a*b) }
	5. To call the Lambda expressions, Functional interface reference is required. Whereever the fuctional interfaces are there, threr only Lambda expressions can be used.
		

How to call/Invoke the lambda expression:
-------------------------------------------
	Functional Interfaces
	---------------------
		1. An interface is having single Abstract method(SAM) is called Functional interface.
		2. It is the concept where you can use Lambda expression.
		3. If there is no functional interface, we can't use lambda expression.
		4. Special annotation came indicate explicitly for funcation interface is @FunctionalInterface. It is optional to annotate if it has only one Abstrace method.
		5. In general, interface methods are public and abstract by default. This rule is gone after Java 8. An interface can have concrete methods also.
		6. If Lambda expression is not there, we need to create a child class which imlements the interface(functional), override the methods providing implementation and then invoke the class method from calling class.
		Eg :
			Interface Interf {
				void m1();
			}
			class Demo implements Interf {
				public void m1() {
					sop("m1 implementation");
				}
			}
			class Test {
				public static void main(String[] args) {
					Interf intf = new Demo(); // or Demo d = new Demo();
					intf.m1(); // or d.m1();
				}
			}
			
	These interfaces contains only one method:
		Runnable==> run ()
		Callable==> call()
		Comparable==> compareTo()

From Java 1.8
	1. Inside interface, we can have Default and Static methods also with implementation, the functional interface restriction is only applicable for only Abstract method.
	2. Functional interface can have any number of static and default methods.
	3. Child interface is also FunctionalInterface when it does't have any methods but it extends the FunctionalIterface parent class.
		@FunctionalInerface
		interface A {
			public void m1();
		}
		@FunctionalInterface
		interface B extends A {
		}
	4. To invoke Lambda expression, some reference must be required. That is functional inteface.
	
Examples:
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
	
	
