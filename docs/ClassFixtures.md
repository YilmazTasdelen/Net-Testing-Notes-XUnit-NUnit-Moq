# Class Fixtures

As we can see in the previous test, we create the same class over and over again in every test method. This means we are wasting resources because it takes time and resources.

- Instead of creating the same object multiple times, we can create a new class and reuse it every time we need that object.

 - Let's add a class:

```clike
public class CalculatorFixture : IDisposable{
    public Calculator Calc => new Calculator();

    public void Dispose(){
        //clean
    }
}
```
- We implement Disposable interface because we will have a dispose method in case wee need clean up some resources.

- classFixture dosnt have any method its just marker interface. Its a technique that you mark your classes with interface so use reflection to get some extra information for your classes.


- so we add and we need to have an access to an instance of calculator fixture in our test.
```clike
public class CalculatorTest : IClassFixture<CalculatorFixture> {

    private readonly CalculatorFixture _calculatorFixture;

    public CalculatorTest (CalculatorFixture alculatorFixture){
    _calculatorFixture = calculatorFixture;
    }
}
```
- so this calculator fixture that injected via the constructure of our test class as singleton class. so we dont have to crete new instances of it.

```clike
public class CalculatorTest : IClassFixture<CalculatorFixture> {

    private readonly CalculatorFixture _calculatorFixture;

    public CalculatorTest (CalculatorFixture alculatorFixture){
    _calculatorFixture = calculatorFixture;
    }


    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboDoesNotIncludeZero(){
        var cal = _calculatorFixture.Calc;
        Assert.All(cal.FiboNumbers, n => Assert.NotEqual(0, n));
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboInclude13(){
        var cal = _calculatorFixture.Calc;
        Assert.Contains(13, cal.FiboNumbers);
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboDoesNotInclude4(){
        var cal = _calculatorFixture.Calc;
        Assert.DoesNotContain(4, cal.FiboNumbers);
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void CheckCollection(){
        var cal = _calculatorFixture.Calc;
        var expectedCollection = new List<int> { 1, 1, 2, 3, 5, 8, 13 };
        Assert.Equal(expectedCollection, cal.FiboNumbers);
    }
}
```
