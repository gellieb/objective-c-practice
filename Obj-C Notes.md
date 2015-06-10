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
            + ```stringWithFormat:``` expects arguments for each *placeholder* in the format string. If the number of arguments doesn't equal the number of placeholders => compiler error
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

##Blocks
+ Any code inside curly-braces ```^{}```
    + ```^{
  NSLog(@"Hello from inside the block");
};```

+ Assign a block to a variable (different syntax)-- prepend with ```^``` not ```*```
    + ```^logMessage =  ^{
  NSLog(@"Hello from inside the block");
};```
+ **Return value**
    + ```void (^logMessage)(void) = ^{
  NSLog(@"Hello from inside the block");
};```
        + specify type of return object -- *use ```void``` if the block doesn't return anything*
        + must wrap variable name, including ^, in parentheses
        + specify the types of arguements this block accepts. If block doesn't accept any arguments, use ```void``` again
+ **Blocks with arguments**    
    + *ex: Arguments are NSUIntegers (not objective-c objects)*
    
    ```
    void (^sumNumbers)(NSUInteger, NSUInteger) = ^(NSUInteger num1, NSUInteger num2){

      NSLog(@"The sum of the numbers is %lu", num1 + num2);
    };
    ```
 *Note*: **Left side of ```=```** : arguments defined only with their TYPES ```(NSUInteger, NSUInteger)```
         **Right side** : defined with TYPES AND NAMES ```(NSUInteger num1, NSUInteger num2)```
    
    + To invoke ```sumNumbers``` block:
    ```sumNumbers(45,89);```
    
    + *ex: Arguments are NSArray*
    
    ```
    void (^logCount)(NSArray *) = ^(NSArray *array){
  NSLog(@"There are %lu objects in this array", [array count]);             ///[array count] returns NSUInteger
};
logCount(@[@"Mr.", @"Higgie"]);
logCount(@[@"Mr.", @"Jony", @"Ive", @"Higgie"]);
```

+ **Enumerate with Blocks** 
    + ```enumerateObjectsUsingBlock:``` message on ```NSArray```
    
    ```
    void (^enumeratingWords)(NSString *, NSUInteger, BOOL *) = 
  ^(NSString *word, NSUInteger index, BOOL *stop){
    NSLog(@"%@ is a funny word", word);
  };
                         
    [funnyWords enumerateObjectsUsingBlock:enumeratingWords];
    ```
    + Must include the ``NS`UInteger`` and ```BOOL``` arguments.


##Classes
###General attributes and conventions
+ Define interface
    + A class interface is a list of available methods and properties. Needs basics like ```alloc``` or ```init```, ```description```, ```copy```, etc.
    
    ```
    @interface ClassName
    @end
    ```
+ Inheritance
    + the root base class is ```NSObject``` and classes like ```NSDictionary```, ```NSString```, ```NSArray``` all inherit from it to respond to a common set of messages

    ```
    @interface ClassName : NSObject
    @end
    ``` 
+ Properties
    + properties are defined by writing ```@property```.
    + need both a type and a name
    + properties are like variables that attach to an object, but allow the object or anyone using the object have access to that variable
    + set ```greeting``` property like this:
    
    ``` 
    ClassName *className = [[ClassName alloc] init];
    className.greeting = @"Hello";
    ```
    
    + properties in an object accessed using the *dot* notation: ```<object>.<property>``` ***HOWEVER*** use message sending
        + ```className.greeting``` calls **```[className greeting]```**
        + ```className.greeting = @"Hello"``` calls **```[className setGreeting:@"Hello"]```**
   + 
    
  
###Class implementation
+ The class implementation is where properties and methods get made
+ Properties are special because they are *automatically* implemented once the class is implemented. Not the case with methods.
    ```
    @implementation ClassName
    @end
    ```
###File Organization
+ **DO NOT PUT THE HEADER AND IMPLEMENTATION IN THE SAME FILE**    
+ Convention:
    + header file: ```ClassName.h```
        
        ```
        ClassName.h 
        
        @interface ClassName : NSObject
        @property NSString *greeting;
        @property NSString *farewell;
        @end
        ```
    + implementation file: ```ClassName.m```
        
        ```
        ClassName.m
        
        #import "ClassName.h"
        
        @implementation ClassName
        @end
        ```
+ must *import* the implementation file ```ClassName.h``` to ```ClassName.m``` because we separated the implementation from the interface file. The ```#import``` command will find the appropriate file and "copy" it into the interface file.
+ 
   
###Custom Methods
_Declaring the ```speak``` method in header_

```
ClassName.h

@interface ClassName : NSObject 

// list of properties

-(void)speak;

@end
```

_Breakdown_

    1. begin with ```(-)``` 
    2. follow with type in parentheses of return value ```(void)```
    3. declare name of custom method ```speak```

_Implement ```speak```method in implementation file_

```
ClassName.m

#import "ClassName.h"

@implementation ClassName
-(void) speak;
{
    NSLog(@"Speaking now");
}
@end
```

_Breakdown_

    1. ```-(void) speak;``` stays exactly the same in the implementation file
    2. directly followed by ```{}``` which wraps the code that will be executed every time the ```speak``` message is sent to a ```ClassName``` object.


