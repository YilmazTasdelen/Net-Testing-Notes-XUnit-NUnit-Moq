# Assert Numeric

this is the class we will test 
```
public class Calculator{

    public int Add(int a, int b){
        return a+ b;
    }

     public int AddDouble(double a, double b){
        return a+ b;   
    }
}
```

Testing the class 
```
public CalculatorTests{

    public void Add_GivenTwoIntValues_ReturnsInt(){
        var calc = new Calculator();
        var resuşt = calc.Add(1,2);
        Assert(3,result);
    }

     public void Add_GivenTwoDoubleValues_ReturnsDouble(){
        var calc = new Calculator();
        var resuşt = calc.AddDouble(1.2,3.5);
        Assert(4.7,result);
        // Assert(4.7,result,1); // round up by one decimal value
    }
}
```

