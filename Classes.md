#Classes
##General attributes and conventions
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
    
  
##Class implementation
+ The class implementation is where properties and methods get made
+ Properties are special because they are *automatically* implemented once the class is implemented. Not the case with methods.
    ```
    @implementation ClassName
    @end
    ```
##File Organization
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

   
##Custom Methods
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
