# what is XUnit.Net 

- unit testing tool 
- free and open source 
- written by inventor of Nunit 2
- used to test c# F# and VB.net
- supports .net .net core and Xamarin


# Features

- Support multiple platform 
- paralel test execution 
- Supports data driven tests
- is design to be extensible you can add mor data types attiributes assests to extract .net and using alongside with other testing frameworks.
- default unit testing tool in vs for .net core 

# Phases of Unit Testing 

> Arrange : thats when you  create an instance of your test subject.

> Act : when you basically make some calls, run some code, do some logic

> Assert: compare phase.


## first Example 

```
// Test we dont focus on naming fur first example 
[Fact]
public void TestAdd(){
    Assert.True(True);
   // Assert.Equal(1,2); // expected val , actual val
}

```