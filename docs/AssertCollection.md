# Assert Collections

class
```
public class Calculations{

List<int> FiboNumbers = new List<int>{1,1,2,3,5,8,13};
}
```


testing 
```
[Fact]
public void FiboDoesNotIncludeZero(){
    var cal = new Calculations();
    Assert.All(calc.FiboNumbers, n=> Assert.NotEqual(0,n));
}
```


```
[Fact]
public void FiboInclude13(){
    var cal = new Calculations();
    Assert.Contains(13,calc.FiboNumbers);
}
```

```
[Fact]
public void FiboDoesNotInclude4(){
    var cal = new Calculations();
    Assert.DoesNotContains(4,calc.FiboNumbers);
}
```

```
[Fact]
public void CheckCollection(){
    var expectedCollection = = new List<int>{1,1,2,3,5,8,13};
    Assert.Equal(expectedCollection,calc.FiboNumbers);
}
```