---
layout: post
title: "Single Method Unit Tests"
description: ""
category:
tags: [junit]
---
Often, I've found myself coming across unit tests that appear to be testing all scenarios within a single method. Common places I seem to find these types of tests are: Mappers, Repositories, and Factories. If the code was truly test driven, then there may be absolutely nothing wrong with the solution. The question that  I'd propose: Could we improve the readability and maintainability by having each scenario in a separate test?

In my example I decided to use a mapper. Which will be responsible for mapping between a domain and a view object. To keep focus on potential test readability improvements, only test code will be provided.

My code below currently contains a single test scenario that has the responsibility of testing that every field was correctly mapped by the mapper.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {

    @Test
    public void mapPersonToPersonView() {
        Person person = new Person();
        person.setFirstName("Skylar");
        person.setLastName("Watson");
        person.setHeight(65);
        person.setAge(38);

        PersonView view = new PersonMapper().map(person);

        assertEquals("Skylar Watson", view.getDisplayName());
        assertEquals("5'5", view.getHeight());
        assertEquals(38, view.getAge());
    }
}
```

A new test has been created as an initial step in separating the individual assertions from the original large test. Since the test has a single focus, a name can be provided that more accurately describes its behavior.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {

    @Test
    public void mapPersonToPersonView() {
        Person person = new Person();
        person.setHeight(65);
        person.setAge(38);

        PersonView view = new PersonMapper().map(person);

        assertEquals("5'5", view.getHeight());
        assertEquals(38, view.getAge());
    }

    @Test
    public void mapFirstAndLastNameToDisplayNameOnView() {
        Person person = new Person();
        person.setFirstName("Skylar");
        person.setLastName("Watson");

        PersonView view = new PersonMapper().map(person);

        assertEquals("Skylar Watson", view.getDisplayName());
    }
}
```

Two tests are now defined and both are creating a new instance of the mapper. We can eliminate this slight duplication by extracting this functionality into a setup method.

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {
    private PersonMapper mapper = new PersonMapper();

    @Before
    public void setUp() {
        mapper = new PersonMapper();
    }

    @Test
    public void mapPersonToPersonView() {
        Person person = new Person();
        person.setHeight(65);
        person.setAge(38);

        PersonView view = mapper.map(person);

        assertEquals("5'5", view.getHeight());
        assertEquals(38, view.getAge());
    }

    @Test
    public void mapFirstAndLastNameToDisplayNameOnView() {
        Person person = new Person();
        person.setFirstName("Skylar");
        person.setLastName("Watson");

        PersonView view = mapper.map(person);

        assertEquals("Skylar Watson", view.getDisplayName());
    }
}
```

Continuing with the refactoring I created a separate test to assert the height and age on the  person object. Again, allowing for the test name to be more descriptive of the behavior of the current test.


```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {
    private PersonMapper mapper = new PersonMapper();

    @Before
    public void setUp() {
        mapper = new PersonMapper();
    }

    @Test
    public void mapPersonOnView() {
        Person person = new Person();
        person.setAge(38);

        PersonView view = mapper.map(person);

        assertEquals(38, view.getAge());
    }

    @Test
    public void mapHeightToStringValueOnView() {
        Person person = new Person();
        person.setHeight(65);

        PersonView view = mapper.map(person);

        assertEquals("5'5", view.getHeight());
    }

    @Test
    public void mapFirstAndLastNameToDisplayNameOnView() {
        Person person = new Person();
        person.setFirstName("Skylar");
        person.setLastName("Watson");

        PersonView view = mapper.map(person);

        assertEquals("Skylar Watson", view.getDisplayName());
    }
}
```

Each test is also creating a new instance of a Person. Similar to the PersonMapper, moving the initialization of the Person object to the setup method allows us to remove this slight duplication.

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {
    private PersonMapper mapper;
    private Person person;

    @Before
    public void setUp() {
        mapper = new PersonMapper();
        person = new Person();
    }

    @Test
    public void mapPersonOnView() {
        person.setAge(38);

        PersonView view = mapper.map(person);

        assertEquals(38, view.getAge());
    }

    @Test
    public void mapHeightToStringValueOnView() {
        person.setHeight(65);

        PersonView view = mapper.map(person);

        assertEquals("5'5", view.getHeight());
    }

    @Test
    public void mapFirstAndLastNameToDisplayNameOnView() {
        person.setFirstName("Skylar");
        person.setLastName("Watson");

        PersonView view = mapper.map(person);

        assertEquals("Skylar Watson", view.getDisplayName());
    }
}
```

If you want to take it one step further then you can inline the assertion of the production invocation.

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonMapperTest {
    private PersonMapper mapper;
    private Person person;

    @Before
    public void setUp() {
        mapper = new PersonMapper();
        person = new Person();
    }

    @Test
    public void mapPersonOnView() {
        person.setAge(38);

        assertEquals(38, mapper.map(person).getAge());
    }

    @Test
    public void mapHeightToStringValueOnView() {
        person.setHeight(65);

        assertEquals("5'5", mapper.map(person).getHeight());
    }

    @Test
    public void mapFirstAndLastNameToDisplayNameOnView() {
        person.setFirstName("Skylar");
        person.setLastName("Watson");

        assertEquals("Skylar Watson", mapper.map(person).getDisplayName());
    }
}
```

Although the original code had less lines. It could produce a test failure for a number of reasons. In a larger, more complicated domain that could potentially make it harder to resolve these failures.
