# Sharing Data Across Methods


- we need to create static class to that 

```clike
publicstatic class TestDataShare {
    public static IEnumerable<object[]> IssOddOrEvenData {
        get{
            yield return new object[] {1,true};
            yield return new object[] {200,false};
        }
    }
}

```

- in  our test we use MemberData which accepts 2 parameter, first one is the member name which is name of your property (for this example its IssOddOrEvenData ) and the second one is the name of the class.

> [MemberData(maneof(TestDataShare.IsOddOREvenData),typeof(TestDataShare))]

```clike
[Theory]
[MemberData(maneof(TestDataShare.IsOddOREvenData),MemberType = typeof(TestDataShare))]
[InlineData(200,false)]
public void IsOdd_GivenValue_ReturnsTrue(int value,bool expected){
    var calc = new Calculations();
    result = calc.IsOdd(value);
    Assert.Equal(expected,result);

}
```

