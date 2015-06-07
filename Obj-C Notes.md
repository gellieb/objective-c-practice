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
+ 
    
