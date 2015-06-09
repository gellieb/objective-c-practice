#Objective-C Notes
##Etiquette
+ *Always* prefix strings with "**@**"
+ *Always* end declaration with "**;**"
+ Most types have "mutable" counterparts, ie. ```NSMutableArray```, ```NSMutableString```
+ Each word in the message name followed by a ```:``` = argument
+ Due to long messageNames, wrap lines to make them more readable

##Basic Objects
###Create empty objects (any class)
+ Create empty Obj-C object : ```NSSomeObject *emptyObject = [NSSomeObject someObject];```
+ Create empty Obj-C object with **alloc/init** : ```NSSomeObject *emptyObject = [[NSSomeObject alloc] init];```
    + All classes respond to the ```alloc``` message, which allocates a place in memory to store the object.
    + ```alloc``` returns an object that is unusuable until ```init``` is sent to it. (meaning ```NSString *string = [NSString alloc]```does not work without nesting in ```init```)
    + specific ```init``` methods send the result of ```alloc``` to create objects with data, like the ```initWithString:``` message that makes a copy of a string.
    + Pairing ```alloc``` with an ```init*``` message is very common in Objective-C.


###```NSLog()```
+ outputs whatever is between the () to the console
+ String interpolation : ```NSLog(@"Hello, %@, %@", firstVar, secVar)```
+ 

###```NSString```
+ Variable declaration for strings : ```NSString **variable* = @"blahblah";```
+ ```@""``` syntax is shortcut for creating an object with type NSString. 

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
+ Accessing values : ```people[@"name"];```

##Perform actions
### Calling a method/Sending a message
+ need at least two things - object and message name ```[objectName messageName];```
+ Obj-c has built in objects like ```NSString```, ```NSNumber```, ```NSArray``` can send multiple messages:
    + ```description```
        + always returns ```NSString``` represents the contents of the object that you passed the message to
        + pass message to ```NSString``` = characters in that string
        + pass message to ```NSArray``` = string containing all the values in that array
        + ex: ```NSLog(@"%@", [objectName description])```
        + To store value:
        
        ``` 
        NSArray *foods = @[@"tacos", @"burgers"]
        NSString *result = [foods description];

        NSLog(@"%@", result)```
        
###NSUIntegers
+ Operations cont'd.
   + ```length```
       + ```NSString``` objects accept message called ```length``` that returns the number of characters in the string
       + To store result of length:```NSUInteger aLength = [objName length];```
       + Some variables don't need an asterisk and therefore are treated differently
           + Objective-C objects are defined with the ```*```, whereas C ones are not.
       + To log NSUInteger value:```NSLog(@%lu, [objName length]);```

###NSNumbers
+ Operations
    + Multiplication
        + Cannot multiply variables normally because multiplying with ```*``` is something done *in c*
        + So: convert ```NSNumber``` to ```NSUInteger``` to multiply
    
    ```
    NSNumber *myAge = @25;
    NSNumber *hisAge = @28;
    
    NSUInteger myAgeInt = [myAge unsignedIntegerValue];
    NSUInteger hisAgeInt = [hisAge unsignedIntegerValue];
    
    NSUInteger combinedAge = myAgeInt * hisAgeInt;
    NSLog(@%lu, combinedAge);
    ```
###NSStrings
+ Operations
    1. String Interpolation
        + ```stringWithFormat:```:shorter way of string interpolation
            + ex: ```NSString *fullname = [NSString stringWithFormat:@"%@ %@", firstName, lastName];```
            + ```stringWithFormat:``` expects arguments for each *placeholder* in the format string.
        + ```stringByAppendingString```: Appending 2 strings
            + ex: ```NSLog(@"My name is %@", [firstString stringByAppendingString:lastString]);```

    2. Nested messages
        + ex: ```NSString *fullName = [[firstName stringByAppendingString:@" "] stringByAppendingString:lastName]; ```
    3. Multiple Arguments
        + ```stringByReplacingOccurrencesOfString:___withString:___``` : takes 2 string arguments 
       + ex: ```[fullName stringByReplacingOccurrencesOfString:firstName withString:lastName];```
    4. Copy ```NSString``` (2 ways)
        + ```NSString *someString = [NSString newString];```
        + ```stringWithString:``` : makes a copy of the string passed in
            + ```NSString *copy = [NSString stringWithString: templateString];```
       + ```initWithString:``` : using ```alloc``` to make copy of string passed in 
           + ```NSString *copy = [[NSString alloc] initWithString:otherString];```
    5. 
    


    
