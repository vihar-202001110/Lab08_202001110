# Lab Report

**Name**: _Vihar Shah_  
**ID**: _202001110_  
**Lab**: _08_  
**Objective**: _JUnit Testing in Eclipse_

---

## Creating Java Package and Boa Class

A package _Lab08_ is created to house the _Boa_ class implementation. The **.java** cod for the same is as follows:

```java
package Lab08;

/* represents a Boa Constrictor */
public class Boa {
	private String name;
	private int length; // the length of the boa, in feet
	private String favoriteFood;

	public Boa (String name, int length, String favoriteFood) {
		this.name = name;
		this.length = length;
		this.favoriteFood = favoriteFood;
	}
	public boolean isHealthy() {
		/* returns true if this boa constrictor is healthy */
		return this.favoriteFood.equals("granola bars");
	}
	public boolean fitsInCage(int cageLength) {
		/* returns true if the length of this boa constrictor is
	 	  less than the given cage length */
		return this.length < cageLength;
	}
}
```

## Creating a JUnit Test Class in Eclipse

We can create a JUnit test case for any **.java** file by right-clicking on the file, selecting _new_ and then clicking on _JUnit Test Case_. We create a test case file **BoaTest.java** for **Boa.java** file.

After configuring the test case file, we define the _setUp()_ function as follows

```java
package Lab08;

import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class BoaTest {
	private Boa jen, ken;

	@BeforeEach
	void setUp() throws Exception {
		jen = new Boa("Jennifer", 2, "grapes");
		ken = new Boa("Kenneth", 3, "granola bars");
	}
	@AfterEach
	void tearDown() throws Exception {
	}
	@Test
	final void testIsHealthy() {
		fail("Not yet implemented"); // TODO
	}
	@Test
	final void testFitsInCage() {
		fail("Not yet implemented"); // TODO
	}
}
```

> Note that the methods _testIsHealthy()_ and _testFitsInCage()_ will contain code to test the _Boa_ class methods. These functions along with _tearDown()_ are yet to be implemented.

## Testing _Boa_ class methods

### _isHealthy()_ method

It is important to note that the _isHealthy()_ function does not take any parameters. Due to this, the only test cases possible are to call the method on _Boa_ objects _"jen"_ and _"ken"_.  
Thus, the test cases defined in the _testIsHealthy()_ test function is as follows:

```java
final void testIsHealthy() {
    assertFalse(jen.isHealthy());
    assertTrue(ken.isHealthy());
}
```

> The cases are defined so because _jen_ does not have favoriteFood as _"granola bar"_ which is necessary for boa object to be healthy while _ken_ has favoriteFood as _"granola bar"_.

### _FitsInCage()_ method

The _FitsInCage()_ function takes an integer parameter as input and hence can have a range of test-cases possible.  
Although _jen_ and _ken_ both will be executing the same function definition for _FitsInCage(<cage_length>)_ function call, it is better to call methods from both the instances to ensure independency of the function definition from the instance.

The test-cases defined can thus go as follows:

```java
final void testFitsInCage() {
    // invalid length input
    assertFalse(jen.fitsInCage(-1));
    assertFalse(jen.fitsInCage(-3));

    // cage larger than boa
    assertTrue(jen.fitsInCage(10));
    assertTrue(ken.fitsInCage(6));

    // cage smaller than boa
    assertFalse(jen.fitsInCage(0));
    assertFalse(ken.fitsInCage(1));

    // cage length equal to boa
    assertTrue(jen.fitsInCage(2));
    assertTrue(jen.fitsInCage(3));
}
```

> Here, the test-cases will be broadly divided into two partitions, corresponding to cage length less than _Boa_, cage length greater than _Boa_ and the boundary condition of cage length equal to _Boa_.
> The first two test cases also account for negative lengths which belong to invalid length input and hence must always return false.

## Running the Test Cases

To run the test cases, we simply right-click on the file(_BoaTest.java_ here), click on _Coverage As_, and then _1 JUnit Test_.

![image](https://user-images.githubusercontent.com/123557378/233040908-c781624e-c3ed-4503-adea-7be1aa2272ea.png)

> Here, the last two test cases fail indicating an error in the code. The error occurs in the _isHealthy()_ function which is defined as follows:

```java
public boolean fitsInCage(int cageLength) {
    return this.length < cageLength;
}
```

To correct this error, the actual definition of the function should be like as shown below to account for the fact that the boa can fit in a cage equal to its length (even if not comfortably).

```java
public boolean fitsInCage(int cageLength) {
    return this.length <= cageLength;
}
```

With the modified code, we can see that all the test-case successfully pass now

![image](https://user-images.githubusercontent.com/123557378/233041915-e4c42123-32f8-4f2e-a7a1-af1651daf218.png)

## Adding new Method

we add a new method _lengthInches()_ to return the length of the Boa in inches.

```java
public int lengthInches(){
    return this.length * 12;
}
``
```

The new test cases defined for the same are as follows:

```java
final void testLengthInches() {
    assertEquals(jen.lengthInches(), 24);
    assertEquals(ken.lengthInches(), 36);
}
```
The test case pass successfully as shown below

![image](https://user-images.githubusercontent.com/123557378/233043302-50ee4e3f-c753-4dd8-9e0b-73fb6c51ae58.png)
