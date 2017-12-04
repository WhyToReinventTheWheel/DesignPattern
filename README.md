-----
SOLID
----- 
	S=Single Responsibility Principle
		A software entity (class, method) should have only one reason to change
	O=Open Closed Principle (open for extension, but closed for modification)
		Open closed principle states that the design and writing of the code should be done
		in a way that new functionality should be added with minimum changes in the existing code
	L=Liskov substitution principle
		child classes should never break the parent class type definition.We have to make sure there 
		will be no problems using the subtype or the original class.Without breaking functionality!!!
	I=Interface Segregation Principle(Programe to interface)
		* We can have an abstraction of the system using interfaces
		* it is not good if an interface contains lots of methods
		* no client should be forced to depend on methods it does not use
		* we should break our interfaces in many smaller ones, so they better satisfy the exact 
			needs of our clients
	D=Dependency Inversion Principle
	
------------------
Creational Pattern
------------------

	* StrategyPattern
		* Favor composition over inheritance
		* Programme to interface
		* Example : We can have any Strategy Add, Multiply, devide etc.
		
		public interface Strategy {
			public void operation(int num1, int num2);
		}

		public class Manager implements Strategy{
			private Strategy strategy;
			public void setStrategy(Strategy strategy){
				this.strategy = strategy;
			}
			@Override
			public void operation(int num1, int num2) {
				this.strategy.operation(num1, num2);
			}
		}
		


		