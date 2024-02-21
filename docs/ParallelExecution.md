# Parallel Execution of Tests in xUnit

## Parallel Execution in xUnit
- xUnit runs tests in parallel by default.
- Each test class is treated as a category for parallel execution.

## Introduction of Collection Attribute
- The Collection attribute is used to control the order of test execution.
- Test classes with the same Collection attribute name run sequentially.
- Example: "customer tests" and "customer details test" with the same Collection attribute run sequentially.

## Efficient Test Execution
- Breaking tests into multiple classes enables parallel execution for efficiency.
- Applying the Collection attribute creates categories for sequential execution.

## Ordering Sequential Execution
- Add a class named "test collection order" to the test project.
- Implement the ITestCollectionOrder interface to order test collections.
- Use LINQ expressions to specify criteria for ordering, e.g., class name or category name.

- adding ordering  for the previous example on Collections ; 
```clike
public class TestCollectionOrderer: ITestCollectionOrderer{
    public IEnumarable<ITestCollection> OrderTestCollections(Ienumerable<ITestCollection> testCollections){
        return testCollections.OrderBy(x=>x.DisplayName);
    }
}
```
