Study Notes

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
	
--------------------------
Behavioral Design Patterns
--------------------------

StrategyPattern
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
		
ObserverPattern
	if one object change state all of its dependents are notified automatically
	
	public interface Observer {
		public void update(int pressure, int temperature, int humidity);
	}
	
	public interface Subject {
		public void addObserver(Observer o);
		public void removeObserver(Observer o);
		public void notifyAllObservers();
	}
	
	public class WeatherStation implements Subject{
		private int pressure;
		private int temperature;
		private int humidity;
		private List<Observer> observersList = new ArrayList<>();
		
		@Override
		public void addObserver(Observer o) {
			this.observersList.add(o);
		}

		@Override
		public void removeObserver(Observer o) {
			this.observersList.remove(observersList.indexOf(o));
		}

		@Override
		public void notifyAllObservers() {
			for(Observer observer : this.observersList){
				observer.update(pressure, temperature, humidity);
			}
		}

		public void setPressure(int pressure) {
			this.pressure = pressure;
			notifyAllObservers();
		}
	}

Command Patterns

	4 components: command, receiver, invoker and client
 	
	Command: knows about receiver and invokes a method of the receiver
		Values for parameters of the receiver method are stored in the command !!!
	
	Receiver: does the work itself
	
	Invoker: knows how to execute a command, and optionally does bookkeeping about the
			command execution The invoker does not know anything about a concrete command, 
			it knows only about command interface !!!
	
	Client: The client decides which commands to execute at which points To execute a command, 
			it passes the command object to the invoker object

	// receiver
	public class Light {
		public void turnOn(){
			System.out.println("Lights are on...");
		}
		public void turnOff(){
			System.out.println("Lights are off...");
		}
	}
	// command 
	public interface Command {
		public void execute();
	}

	public class TurnOffCommand implements Command{
		private Light light;
		public TurnOffCommand(Light light){
			this.light = light;
		}
		@Override
		public void execute() {
			this.light.turnOff();
		}
	}
	
	//invoker
	public class Switcher {
		public List<Command> commandList;
		public Switcher(){
			this.commandList = new ArrayList<>();
		}
		public void addCommand(Command command){
			this.commandList.add(command);
		}
		public void executeCommands(){
			for(Command command : this.commandList){
				command.execute();
			}
		}
	}
	
	
TemplatePattern
	In Template pattern, an abstract class exposes defined way / template to execute its methods
	Its subclasses can override the method implementation as per need but the invocation 
	is to be in the same way as defined by an abstract class
	
	public abstract class Algorithm {
		public abstract void initialize();
		public abstract void sorting();
		public abstract void printResults();
		
		public void sort(){
			initialize();
			sorting();
			printResults();
		}
	}
	

	
--------------------------
Creational Design Patterns
--------------------------

Singleton pattern

	public class SingleObject {
		private static SingleObject instance = new SingleObject();
		private SingleObject(){}
		public static SingleObject getInstance(){
			return instance;
		}
		public void showMessage(){
			System.out.println("Hello World!");
		}
	}
	
Factory pattern	

	public interface Algorithm {
		public void solve();
	}
	public class AlgorithmFactory {
		public static final int SHORTEST_PATH = 0;
		public static final int SPANNING_TREE = 1;
		public static Algorithm createAlgorithm(int type) {
			switch (type) {
				case SHORTEST_PATH:
					return new ShortestPath();
				case SPANNING_TREE:
					return new SpanningTree();
				default:
					return null;
			}
		}
	}

Builder pattern
	

DAO : Data Access Object
	public class Student {
	   private String name;
	   private int rollNo;
	}
	
	public interface StudentDao {
	   public List<Student> getAllStudents();
	   public Student getStudent(int rollNo);
	   public void updateStudent(Student student);
	   public void deleteStudent(Student student);
	}
	
--------------------------	
Structural Design Patterns
--------------------------