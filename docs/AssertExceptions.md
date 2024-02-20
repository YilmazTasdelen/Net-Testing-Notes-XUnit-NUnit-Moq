# Assert Exceptions

Class 
```
public class Customer{

    public int GetOrdersByName(string name){
        if(string.IsNullOrEmpty(name)){
            throw new ArgumentException("null exception");
        }
        return 100;
    }

    public string Name => "Test";
    public int Age => 30;
}
```


Testing
```
[Fact]
public viod GetOrdersByNameNotNull(){
    var customer = new Customer();
    Assert.Throws<ArgumentException>(()=>customer.GetOrdersByName(null));
}
```


with more detail of exception
```
[Fact]
public viod GetOrdersByNameNotNull(){
    var customer = new Customer();
    var exception = Assert.Throws<ArgumentException>(()=>customer.GetOrdersByName(null));
    Assert("null exception",exception.Message);
}
```
