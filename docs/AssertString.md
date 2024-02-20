# Assert String Values 

```
public class Names {
    
    public string NickName {get;set;}

    public string MakeFullNames(string firstName, string lastName){
        return $"{firstName} {lastName}";
    }
}
```
testing 
```
public class NameTest{
    
    [Fact]
    public void MAkeFullNameTest(){
        var names = new Names();
        var resut = names.MakeFullName("Test","Name");
        
        Assert.Equal("Test Name",result);
        
        Assert.Equal("Test Name",result,ignoreCase:true); // compare case insensetive matter 

        Assert.Contains("test",result); //test fails its case insensetive 

        Assert.Contains("test",result, StringComparsion.InvariantCultureIgnoreCase); // ignore casing  

        // using regular expression
        Assert.Match("[A-Z]{1}[a-z]+ [A-Z]{1}[a-z]+",resut);
    } 
```
```
    [Fact]
    public void NickName_MustBeNull(){
        var names = new Names();
        Assert.Null(names.NickName);
    }
```
```

    [Fact]
    public void MakeFullName_AlwaysReturnValue(){
        var names = new Names();
        var resut = names.MakeFullName("Test","Name");
        Assert.NotNull(result);
        //or
        Assert.True(!String.IsNullOrEmpty(result));
        //or 
        Assert.False(String.IsNullOrEmpty(result));
    }
}
```