# Constructures and IDisposable

- to add some debugging information add 

```clike
private readonly ITestOutputHelper _testOutputHelper;
_testOutputHelper.WriteLine("Constructor");
```

```clike
public class CalculatorTest : IClassFixture<CalculatorFixture> {

    private readonly CalculatorFixture _calculatorFixture;
    private readonly ITestOutputHelper _testOutputHelper;


    public CalculatorTest (CalculatorFixture alculatorFixture, ITestOutputHelper testOutputHelper){
    _calculatorFixture = calculatorFixture;
    _testOutputHelper = testOutputHelper;

    _testOutputHelper.WriteLine("Constructor");
    }

    [Fact]
    [Trait("Category", "Fibo")]
    public void CheckCollection(){

         _testOutputHelper.WriteLine("CheckCollection Started at {0}",DateTime.Now);
          var expectedCollection = new List<int> { 1, 1, 2, 3, 5, 8, 13 };

         _testOutputHelper.WriteLine("Creating a instance of calculator class");  
        var cal = _calculatorFixture.Calc;
       
         _testOutputHelper.WriteLine("Asserting");
        Assert.Equal(expectedCollection, cal.FiboNumbers);

        _testOutputHelper.WriteLine("Test End");
    }
}
```

> Note: Test methods shouldnt share instance or pass parameter to each other. Each test method should be independent. it can cause error when we do parallel test.


>If you create some objects that require cleanup, for example, if you have a 
- streams memory  
- file stream   
- Http client sockets 
- database connections
- anything like that

 And if you create them in your constructor so that they are alive, like their scope is the class level.
 
 Because if you create them in your method, then when they go out of scope they get cleaned up. But if you create them at the class level, what you need to do is to dispose them because you can get out of memory exceptions.
 
 for example 

```clike
public class CalculatorTest : IDisposable {

    private readonly MemoryStream memoryStream;
    private readonly ITestOutputHelper _testOutputHelper;


    public CalculatorTest ( ITestOutputHelper testOutputHelper){
    _calculatorFixture = calculatorFixture;
    memoryStream = new memoryStream;

    _testOutputHelper.WriteLine("Constructor");
    }

    
    // add this method for object need dispose
    public void Dispose (){
        memoryStream.Close();
    }

}
```

> But then who is going to call this X unit automatically will check to see if your class implements Idisposable and if it does, it will call the dispose method automatically and it will execute your cleanup code and it will clean up any object that you have generated. 