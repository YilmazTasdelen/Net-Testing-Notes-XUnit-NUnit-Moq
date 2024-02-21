# İnline Attiributes

- our class

```clike
public class Calculations {
    public List<int> FiboNumbers = new List<int>{1,1,2,3,5,8,13};

    public bool isOd(int value){
        return(value % 2 ) ==1;
    }
}
```

- test without data driven aproach

```clike
[Fact]
public void IsOdd_GivenValue_ReturnsTrue(){
    var calc = new Calculations();
    result = calc.IsOdd(1);
    Assert.Equal(true,result);
}

[Fact]
public void IsOdd_GivenValue_ReturnsFalse(){
    var calc = new Calculations();
    result = calc.IsOdd(1);
    Assert.Equal(false,result);
}

```


- test with data riven aproach

```clike

[Theory]
[InlineData(1,true)]
[InlineData(200,false)]
public void IsOdd_GivenValue_ReturnsTrue(int value,bool expected){
    var calc = new Calculations();
    result = calc.IsOdd(value);
    Assert.Equal(expected,result);

}


```


