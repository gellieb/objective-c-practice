#Objective-C Notes
##Etiquette
+ *Always* prefix strings with "**@**"
+ *Always* end declaration with "**;**"
+ Most types have "mutable" counterparts, ie. ```NSMutableArray```, ```NSMutableString```

##Basic Objects
###```NSLog()```
+ outputs whatever is between the () to the console
+ String interpolation : ```NSLog(@"Hello, %@, %@", firstVar, secVar)```
+ 

###```NSString```
+ Variable declaration for strings : ```NSString **variable* = @"blahblah";```
+ 

###```NSNumber```
+ Variable declaration for numbers : ```NSNumber **variable* = @1234;```
+ Log number object : ```NSLog(@"%@", variable);```
    + Unlike string objects, you cannot log a NSNumber object by passing it directly to NSLog.
+ 

###```NSArray```
+ Create array : ```NSArray *vars = @[@"var1", @"var2", @"var3"];```
+ Access element : ```NSLog(@"%@", vars[1])```
+ Add to existing array :
    + 1. Assign entirely new array to variable. No longer need the ```NSArray *``` type specifier because previously defined.
    + 2. Use ```NSMutableArray```

###```NSDictionary``` (like hash)
+ Create hash : ```NSDictionary *people = @{@"name": @"Angel", @"surname": @"Baek", @"age": @3};```
+ Accessing values : ```people[@"name"];

##Perform actions
### Calling a method/Sending a message
+ need at least two things - object and message name ```[objectName messageName];```
+ Obj-c has built in objects like ```NSString```, ```NSNumber```, NSArray``` can send multiple messages:
    + ```description```
        + always returns ```NSString``` represents the contents of the object that you passed the message to
        + pass message to ```NSString``` = characters in that string
        + pass message to ```NSArray``` = string containing all the values in that array
        + ex: ```NSLog(@"%@", [objectName description])
###Store the results of message in another variable
``` 
NSArray *foods = @[@"tacos", @"burgers"]
NSString *result = [foods description];

NSLog(@"%@", result)
```


    
