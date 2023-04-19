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

We can create a JUnit test case for any **.java** file by right-clicking on the file, selecting _new_ and then clicking on _JUnit Test Case_. We create a test case file **BoaTest.java** for **Boa.java** file  
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
}
```
