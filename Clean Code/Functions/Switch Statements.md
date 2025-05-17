Created: 2025-05-15 19:38
## Family Tree:
1. Clean Code
2. [[Functions]]
-- -
It's hard to make a small `switch` statement. It's even harder to make a `switch` statement that does one thing, as these code blocks do *N* things by nature.
We can't always avoid `switch` statements, but we can make sure that they're buried in a low level class and never repeated. We do this, of course, with polymorphism.
For exammple:
```java
public Money calculatePay(Employee e) throws InvalidEmployeeType {
	switch (e.type) {
		case COMMISSIONED:
			return calculateCommissionedPay(e);
		case HOURLY:
			return calculateHourlyPay(e);
		case SALARIED:
			return calculateSalariedPay(e);
		default:
			throw new InvalidEmployeeType(e.type)
	}
}
```
There are several problems with this function:
1. It's large.
2. It very clearly does more than one thing.
3. It violates the *Single Responsibility Principle* because there's more than one reason for it to change.
4. It violates the *Open Closed Principle* because it must change whenever new types are added.
But the worst problem with this function is that there are an unlimited number of other functions that will have the same structure. For example, we could have:
```java
isPayday(Employee e, Date date)
```
or
```java
deliveryPay(Employee e, Money pay)
```
or a host of others. All of which would have the same deleterious structure.
The solution to this problem is to bury the `switch` statement in the basement of an *Abstract Factory*, and never let anyone see it.
The factory will use the `switch` statement to create appropiate instances of the derivatives of `Employee`, and the various functions, such as `calculatePay`, `isPayday` and `deliveryPay` will be dispatched polymorphically through the `Employee` interface.
A general rule for `switch` statements is that they can be tolerated if:
1. Appear only once.
2. Are used to create polymorphic objects.
3. Are hidden behind an inheritance relationship so that the rest of the system can't see them.
```java
public abstract class Employee {
	public abstract boolean isPayday();
	public abstract Money calculatePay();
	public abstract void deliveryPay(Money pay);
}
public interface EmployeeFactory {
	public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}
public class EmployeeFactoryImpl implements EmployeeFactory {
	public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
		switch (r.type) {
			case COMMISSIONED:
				return CommissionedEmployee(r);
			case HOURLY:
				return HourlyEmployee(r);
			case SALARIED:
				return SalariedEmployee(r);
			default:
				throw new InvalidEmployeeType(r.type)
		}
	}
}
```