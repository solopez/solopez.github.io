---
date: 2023-03-27 8:00:00
layout: post
title: Unit testing Jest & Jasmine
description: Theory and samples!
language: en
image: "../assets/img/jasmine_jest.jpg"
category: CODE
tags:
  - unit testing
  - jest
  - jasmine
  - humor
author: sol lopez
---

# Unit testing - Jasmine & Jest

How are you doing? Today's post is dedicated to general unit testing taking into account some concepts and experiences in both frameworks: Jasmine and Jest.

## mockReturnValue and mockReturnValueOnce

Let's suppose a scenario where we want to test what happens when a method of some service returns different values.
A classic example we could use would be the following:

```typescript
jest.spyOn(userService, "get").mockReturnValue(0);
```

Now, if we wanted to return other values for different method calls, we can do this:

```typescript
jest
  .spyOn(userService, "get")
  .mockReturnValue(0) // default
  .mockReturnValueOnce(2) // first call
  .mockReturnValueOnce(4); // second call

it("should mock the return value of consecutive calls differently", () => {
  expect(userService.get()).toBe(2);
  expect(userService.get()).toBe(4);
  expect(userService.get()).toBe(0);
  expect(userService.get()).toBe(0);
});
```

As you can see, with the function mockReturnValue we will return by "default" a value, and if we concatenate with the function mockReturnValue**Once**, the once gives us the key that it will only return only once that value, and it will be according to the order that we give it.
As we can see in the exercise, the first call will return 2, then 4 and then, as many times as we keep calling it, it will always return 0 (default).

## **mockImplementation** and **mockImplementationOnce**

In the same way we did before, we could mock our spy by concatenating different behaviors for each time the method is called/invoked.
That is, we could do exactly the same exercise above but using the mockImplementation() function, or also customize it a bit if we wanted to, for example:

```typescript
it("Should mock the return value of consecutive calls differently", () => {
  userService.get = jest
    .fn()

    .mockImplementation(() => 0) // default

    .mockImplementationOnce((num) => num + 10) // first call

    .mockImplementationOnce((num) => num + 20); // second call

  expect(userService.get(10)).toBe(20);

  expect(userService.get(10)).toBe(30);

  expect(userService.get()).toBe(0);

  expect(userService.get()).toBe(0);
});
```

As we can see in this exercise, it is possible to perform a different sum in each call or invocation to our method. The useful thing about mockImplementation is that by receiving a function as a parameter, we will be able to implement what corresponds and not just return values like the mockReturnValue() functions.

## Jasmine

This same exercise of returning different values in consecutive calls is also possible in Jasmine, using the **returnValue** and **returnValues** functions.
In the case of returnValue() we will return a single value, while in the case of returnValues() we will be able to return different values separated by comma and in that order.
It would look like this:

```typescript
spyOn(userService, "get").and.returnValues(2, 4, 0);
```

Also, if we wanted to get the equivalent of mockImplementation(), in Jasmine we could do it with the function callFake(), which also receives as parameter a function:

```typescript
spyOn(obj, "methodName").and.callFake(customImplementation);
```

## Spies cleaning

![Create comics meme "the shining memes, here's johnny, Jack Nicholson the  shining door" - Comics - Meme-arsenal.com](https://www.meme-arsenal.com/memes/06ec1715360623bb409a354cd5f36bd1.jpg)
In Jest, if we would like to clean the spies that we are mocking in each scenario, we can use one of the 3 functions provided by this framework: mockClear(), mockReset() and mockRestore().
Let's see how they work

```typescript
const spy = jest.spyOn(userService, "get");

spy.mockImplementation(() => "mocked implementation");

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //mocked implementation

spy.mockClear();

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //mocked implementation

spy.mockReset();

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //undefined (reset destroys mockImplementation)

spy.mockRestore();
userService.get();
expect(spy).toHaveBeenCalledTimes(0); //Its me Mario!(real implementation)
```

The first case, **mockClear()** will clean all the tracking information that our spy stores, but it will keep the same characteristics of our spy. In this case, it will continue to return what we mock using _mockImplementation()_.

The second case, **mockReset()**, will not only remove the tracking information as well as the clear, but will also destroy the mock we implemented, and replace it with undefined. Which means that in order to continue using that spy, we will have to re-mock it according to what we need to test.

The third case, **mockRestore()**, will stop being a spy, and will invoke our real method and implementation. That is why in this case, the \*_toHaveBeenCalledTimes_(0)\* will be 0, since the spy is not called and the real implementation of the method would be executed directly.

It is also possible that we use these 3 functions but general for all the spies, instead of each one, to be able to invoke them for example, in the before/afterEach and before/afterAll, this way:

```typescript
jest.clearAllMocks();

jest.resetAllMocks();

jest.restoreAllMocks();
```

## Spies: Jasmine vs Jest

A fundamental issue to keep in mind is that in Jasmine, and in most testing frameworks, doing the following:

```typescript
    spyOn(obj, ‘methodName’); //!real function
```

We see that it is enough to create the spy of a method, to mock it, and that the real implementation is not accessible by this one. In such a way that when we invoke our method, it will not access its real implementation, as if it were empty.

However, in Jest, it is the opposite:

```typescript
    jest.spyOn(obj, ‘methodName’); //real function
```

When we create the spy, it is not enough and if we invoke the method, the real implementation is the one that is going to fetch. That's why in the case of Jest, we must apply some of the mocking functions provided by the framekwork.

## Mocking dependencies

![MOCKS: What are they? When should you use them?](https://media.licdn.com/dms/image/C4E12AQFFdpXrcMl4hg/article-cover_image-shrink_600_2000/0/1520175912857?e=2147483647&v=beta&t=M-q9AA8fseLznsSmQyfc8il3RgYH38ycq07V5J1vd5U)
To mock our dependencies/services, just inject it into our tests in one of the following ways:

```typescript
    TestBed.configureTestingModule({
    providers: [

    { provide:  service, useClass:  serviceClassMock }

    { provide:  service, useValue: { serviceMock } }

    { provide:  service, useFactory: () => {
        if (IS_A) {
          return new A();
        } else {
          return new B();
        }
      }
```

In the first case _useClass_ , we will use an instance of a class. In the second case _useValue_, we will use an object or static value. And in the third case _useFactory_ we will use a function that can produce the value to inject.

In the case of a dependency that is not injected by constructor, but directly in a component, in this way:

```typescript
    @Component({

    templateUrl:  './main.component.html',

    styleUrls: ['./main.component.scss'],

    providers: [service]

    })
```

In order to scoped this dependency, we will need to apply the overrideComponent() function, as follows:

```typescript
    TestBed.configureTestingModule({

    //imports, declarations, providers, schemas

    })

    .overrideComponent(MainComponent, { set: { providers:

    [{ provide:  service, useClass:  serviceClassMock }]

    }})

    .compileComponents()});
```

By implementing this function, we will be able to inject our dependency with its respective mock.

## Conclusion

Having seen some concepts and experiences to continue building and mocking our tests, it is also necessary to keep in mind some points when writing tests:

- Simple, clear and descriptive tests in the messages: the idea is that we are so clear that the next person who reads our test, can easily interpret what is being tested and does not have to go read the entire suite of tests to be able to do so.
  ![Meme: "I think it is crystal clear" - All Templates - Meme-arsenal.com](https://www.meme-arsenal.com/memes/4b6a7e7edd3a8872aedda1060b276b87.jpg)

- Isolated tests, without dependencies or order of execution: always remember to mockear all dependencies and that our tests should always yield the same results, regardless of the order in which they are executed.
- AAA Rule: Arrange, Act, Assert: for better readability it is useful to be able to break down and separate the 3 actions in each of our tests.
- Expose bugs: from our unit tests, it is possible to recreate the scenarios in order to reproduce the bugs that have been detected, revealing them, it can be very helpful to detect where the problem is and thus be able to fix the code. It also gives us more security to have the unit test of the scenario we are fixing to ensure that such a bug does not come back to life :)
  ![Don't be a mindless zombie this Halloween](https://www.evolutionrecruit.co.uk/wp-content/uploads/2018/10/zombie-hands-emerging-from-the-grave_4jxo6n6q__F0010.png)
  Happy coding!
