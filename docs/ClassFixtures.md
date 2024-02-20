# Class Fixtures

As we can see in the previous test, we create the same class over and over again in every test method. This means we are wasting resources because it takes time and resources.

Instead of creating the same object multiple times, we can create a new class and reuse it every time we need that object.

Let's add a class:

```clike
public class CalculatorFixture{
    public Calculator Calc => new Calculator();
}
```

```clike
public class CalculatorTest {

    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboDoesNotIncludeZero(){
        var fixture = new CalculatorFixture();
        var cal = fixture.Calc;
        Assert.All(cal.FiboNumbers, n => Assert.NotEqual(0, n));
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboInclude13(){
        var fixture = new CalculatorFixture();
        var cal = fixture.Calc;
        Assert.Contains(13, cal.FiboNumbers);
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void FiboDoesNotInclude4(){
        var fixture = new CalculatorFixture();
        var cal = fixture.Calc;
        Assert.DoesNotContain(4, cal.FiboNumbers);
    }
    
    [Fact]
    [Trait("Category", "Fibo")]
    public void CheckCollection(){
        var fixture = new CalculatorFixture();
        var cal = fixture.Calc;
        var expectedCollection = new List<int> { 1, 1, 2, 3, 5, 8, 13 };
        Assert.Equal(expectedCollection, cal.FiboNumbers);
    }
}
```
