---
title: Test Suites With Jasmine
date: 2022-10-12 18:00:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [programming, browser, angular, testing]
---

## Definition

What is Jasmine? - Jasmine is a test framework provides for JavaScript based framework like Angular, AngularJS and Node.js. In Angular, every newly created project are ships with Jasmine. Jasmine helps developer write and execute unit test and integration test.

Jasmine consist three important features:

> - Library with classes for building tests.
> - Test execution engine
> - Reporting engine to generate results for the test execution.
{: .prompt-info }

## Test Suites & Specs

- For Jasmine, a test consist one or more "suites". A suite is use to holds one or more specifications or spec to describe a piece of code that are being tested.

- A suite is declared with a "describe" function block, while specs is declared with it block:

```js
 describe('Suite description', () => {
  it('Spec description', () => {
   /*...*/
  });
  /*... more specs ...*/
 });
 
 /*... more suites ...*/
```

### Suite (describe:Suite)

- Describe is a function block that holds two parameters:
  - Human-readable string name to describe the name of a features or class under test. For Example:

    ```js
    describe('CounterComponent', /*...*/)   // CounterComponent is a class
    ```

  - A function containing the suite definition or the content of the test.
  - Describe block can be nested to define the suites. For Example:

    ```js
    describe('Suite description', () => {
    describe('Nested 1', () => {
    /*...*/
    });
    describe('Nested 2', () => {
    /*...*/
    });
    });
    ```

### Specifications or specs (it:Spec)

- Specifications is function blocks that holds two parameters same as Suite:
  - Human-readable name to summarize what this specs is all about. For Example:

    ```js
    it('Specs description', /*...*/)
    ```

  - Function containing specification code. For Example:

    ```js
    it('Specs description', () => {
    /*...*/
    });
    ```

## Structure of test

Inside "it" or specs block lies the actual testing code. Testing code typically consist three phases which is **Arrange, Act and Assert**.

### Arrange

- Preparation and setup phase, to define what dependencies is needed for the test. For example, class under test is instantiated, Setting up dependencies, spies and fakes are created.

### Act

- Phase when the Interaction with code under test happens. For example, method is being called or HTML element in the DOM is clicked.

### Assert

- Phase where the code is being checked, tested and verified. For example, the actual output is compared to the expected result. This phases of a test is fundamentally similar with Behavior-Driven Development (BDD)'s test phases which is called **Given, When and Then**

## Expectations

In the Assert phase, the test is being compare between the actual output and the expected result. If they are  similar, the test passes. If they are not, the test fails.

Primitive example without testing tools:

```js
 const expectedValue = 5;
 const actualValue = add(2, 3);

 if (expectedValue !== actualValue) {
  throw new Error (
   `Wrong return value: ${actualValue}. Expected: ${expectedValue}`
  );
 }
```

In Jasmine spec, allow us to make expectation for the Assert phase much easier by using The **expect** function with a **matcher**.

```js
 const expectedValue = 5;
 const actualValue = add(2,3);

 expect(actualValue).toBe(expectedValue);
```

## Efficient test suites

- In the Arrange phase, not just you can instantiate the class under the test, setting up fakes and spies or setting up dependencies.
- You also have the ability to setup Jasmine to take particular action to the code before and after each spec or before and after all specs. This actions is being taken through the four unique function blocks.
- This four functions consist, **beforeEach, afterEach, beforeAll and afterAll**. Below shows how Jasmine implement this four functions for testing:

```js
 describe('Suite description', () => {
  beforeAll(() => {
   console.log('Called before all specs are run');
  });
  afterAll(() => {
   console.log('Called after all specs are run');
  });

  beforeEach(() => {
   console.log('Called before each spec is run');
  });
  afterEach(() => {
   console.log('Called after each spec is run');
  });

  it('Spec 1', () => {
   console.log('Spec 1');
  });
  it('Spec 2', () => {
   console.log('Spec 2');
  });
 });
```

- Above suite has two specs and defined shared setup function, below snippet shows the output:

```markdown
 Called before all spec are run
 Called before each spec is run
 Spec 1
 Called after each spec is run
 Called before each spec is run
 Spec 2
 Called after each spec is run
 Called after all spec are run
```

---

## Sources

1. [Test suites with Jasmine](https://testing-angular.com/test-suites-with-jasmine/#structure-of-a-test)
2. [Getting started with Jasmine](https://jasmine.github.io/tutorials/your_first_suite)
