# Assert Object Types

Base Class 
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

Sub Class
```
public class LoyalCustomer: Customer{
    public Discount {get;set;}
    
    public LoyalCustomer(){
        Discount = 10;
    }

    public int GetOrdersByName(string name){
        return 101;
    }

} 
```
Class Factory 
```
public class CustomerFactory{
    public static Customer CreateCustomerInstance(inr orderCount){
        if(orderCount <= 100){
            return new Customer();
        else
            return new LoyalCustomer();
        }
    }
}
```
Testing 
```
[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = CustomerFactory.CreateCustomerInstance(102);
    Assert.IsType(typeof(LoyalCustomer),customer);    
}
```
more of detail
```
[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = CustomerFactory.CreateCustomerInstance(102);
    var loyalCustomer = Assert.IsType<LoyalCustomer>(customer);
    Assert.Equal(10,LoyalCustomer.Discount);    
}
```