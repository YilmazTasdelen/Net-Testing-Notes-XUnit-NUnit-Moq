# Extarnal Data Source

- DataSource is IsOddOrEvenTestData

```clike
1,true
2,false
```

- our test data sharing class

```clike
publicstatic class TestDataShare {
    
    public static IEnumerable<object[]> IssOddOrEvenData {
        get{
            yield return new object[] {1,true};
            yield return new object[] {200,false};
        }
    }

    public static IEnumarable<object[]> IsOddOrEvenExternalData{
        get{
            var lines = System.IO.File.ReadAllLines("IsOddOrEvenTestData.txt");

            return lines.Select(x=> {
                var lineSplit = x.Split(',');
                return new object [] {
                    int.Parse(lineSplit[0]),
                    bool.Parse(lineSplit[1])
                }
            })
        }
    }
}

```

- after adding new property to TestDataShare class we update our MemberData propert to apply changes.

```clike
[Theory]
[MemberData(maneof(TestDataShare.IsOddOrEvenExternalData),MemberType = typeof(TestDataShare))]
public void IsOdd_GivenValue_ReturnsTrue(int value,bool expected){
    var calc = new Calculations();
    result = calc.IsOdd(value);
    Assert.Equal(expected,result);

}
```





