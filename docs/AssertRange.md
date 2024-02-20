# Assert Range Of Values

class

```
public class Customer{
    public string Name => "Test";
    public int Age => 30;
}
```

testing 

```
[Fact]
public void CheckNameNotEmpty(){
    var customer = new Customer();
    Assert.NotNull(Customer.Name);
    Assert.False(string.IsNullOrEmpty(customer.Name));
}
```


```
[Fact]
public void CheckLegiForDiscount(){
    var customer = new Customer();
    Assert.NotNull(Customer.Name);
    Assert.InRange(customer.Age,25,40);
}
```



