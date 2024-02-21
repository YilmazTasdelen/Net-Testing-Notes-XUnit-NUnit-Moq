# Custom Attiributes

- to writing your own custom attiribute for sharin data. To do that we need to create new class in our test project.


```clike
public class IssOddOrEvenDataAttiribute : DataAttiribute{

    public override IEnumerable<object[]> GetData{
            yield return new object[] {1,true};
            yield return new object[] {200,false}; 
    }
}
```

- our test  using [IssOddOrEvenDataAttiribute]

```clike
[Theory]
[IssOddOrEvenDataAttiribute]
public void IsOdd_GivenValue_ReturnsTrue(int value,bool expected){
    var calc = new Calculations();
    result = calc.IsOdd(value);
    Assert.Equal(expected,result);

}

```