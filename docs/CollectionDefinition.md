# Collection Definition

> We learned that we can share the test subject or anything that we have to just constantly create in every test method across multiple methods by using a class fixture. 

> We can take this even further and share some objects across multiple test classes.

- so we creating an instance of customer class in every single test method in every test class.



Testing class 1  
```clike
public class CustomerTest1Class(){
[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = CustomerFactory.CreateCustomerInstance(102);
    Assert.IsType(typeof(LoyalCustomer),customer);    
}
}
```
Testing Class 2 
```clike
public class CustomerTest2Class(){
[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = CustomerFactory.CreateCustomerInstance(102);
    var loyalCustomer = Assert.IsType<LoyalCustomer>(customer);
    Assert.Equal(10,LoyalCustomer.Discount);    
}
}
```

> Now, it would be good if I could have only one instance of customer, but then I could share it not only across the test methods within one test class, but across all test classes that are related together.

> We do that by applying an attribute called collection and also providing a name for the collection.

- Add a Class Fixture

```clike
public class CustomerFixture{
    public Customer Cust => new Customer();
}

```



- So if this class has a collection with the name customer, this definition will apply on those classes
- Create Collection 

```clike

[CollectionDefinition("Customer")]
public class CustomerFixtureCollection : ICollectionFixture<CustomerFixture>{
    public Customer Cust => new Customer();
}

```
- So by doing this, X unit will understand that this class should be applied to all collections that have the same name.

- Now how do we relate this class to our fixture class via a collection fixture interface and then we pass the customer fixture to a collection fixture because it's generic and a collection fixture but has no method to implement. It's a marker interface.

Testing class 1  
```clike
[Collection("Customer")]
public class CustomerTest1Class{
    private readonly CustomerFixure _customerFixure; 
    public CustomerTest1Class(CustomerFixure customerFixure){
        _customerFixure= customerFixure;
    }

[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = _customerFixure.Cust.CreateCustomerInstance(102);
    Assert.IsType(typeof(LoyalCustomer),customer);    
}
}
```
Testing Class 2 
```clike
[Collection("Customer")]
public class CustomerTest2Class{

    private readonly CustomerFixure _customerFixure; 
    public CustomerTest2Class(CustomerFixure customerFixure){
        _customerFixure= customerFixure;
    }
[Fact]
public void LoyalCustomerForOrdersGreaterThan100(){
    var customer = _customerFixure.Cust.CreateCustomerInstance(102);
    var loyalCustomer = Assert.IsType<LoyalCustomer>(customer);
    Assert.Equal(10,LoyalCustomer.Discount);    
}
}
```