#Self, Methods, Properties, Instance Variables
+ Consider this ```self``` a "magic variable" that is provided to your method definitions by the internals of Objective-C.
+ Example: Coffee

--- 
+ Coffee.h

```
@interface Coffee : NSObject

@property NSString *brand;
@property NSString *acidityLevel;

- (void) pour;

@end
```
---

ex: Coffee.m using ```self```

```
#import "Coffee.h"

@implementation Coffee

- (void) pour;
{
    NSlog(@"Pouring %@", self)                      // Pouring <Coffee: 0x100108240>                       
                                                    // The string description of a Coffee object located at the memory address of 0x100108240.
}
@end
```

##Log property instead of ```self```

+ Coffee.m

```
#import "Coffee.h"

@implementation Coffee
-(void)pour;
{
    NSLog(@"Pouring some %@", [self brand]);        // "Pouring some Stumptown"
}
@end
```

+ Example use:

```
#import "Coffee.h"

Coffee *coffeePot = [[Coffee alloc] init]
coffeePot.brand = @"Stumptown"

[coffeePot pour];                                    // "Pouring some Stumptown"
```
##Method with return values
1. Update the return value type of the method in the header file with the correct return type. It is no longer void.

    + Coffee.h

    ```
    @interface Coffee : NSObject

    @property NSString *brand;
    @property NSString *acidityLevel;

    - (NSString *) pour;

    @end
    ```

2. Add return message to method in implementation file
    + Coffee.m
    
    ```
    #import "Coffee.h"

    @implementation Coffee
    - (NSString *) pour {
        NSString *message = [NSString stringwithFormat:@"Pouring the coffee from %@", self.brand];
        return message;
    }
    @end
    ```
3. Update code to assign the result of the method message 
    + Example code:

    ```
    #import "Coffee.h"
    
    Coffee *coffeePot = [[Coffee alloc] init];
    coffeePot.brand = @"Stumptown";
    
    NSString *coffeeLabel = [coffeePot pour];
    
    NSLog(@"%@", coffeeLabel)
    ```
    
##Declare method with arguments

1. Change method declaration to take a single argument in the header
    + Coffee.h
    
    ```
    @interface Coffee : NSObject

    @property NSString *brand;
    @property NSString *acidityLevel;

    - (NSString *) pour:(NSString *)warning;            //warning = argument
    @end
    ```
2.  Update method implementation
    + Coffee.m
    
      ```
    #import "Coffee.h"

    @implementation Coffee
    - (NSString *) pour:(NSString *)warning;
    {
        NSString *message = [NSString stringwithFormat:@"Pouring the coffee from %@. %@", self.brand, warning];
        return message;
    }
    @end
    ```

3. Update code to assign the result of the method message 
    + Example code:

    ```
    #import "Coffee.h"
    
    Coffee *coffeePot = [[Coffee alloc] init];
    coffeePot.brand = @"Stumptown";
    
    NSString *coffeeLabel = [coffeePot pour:@"Watch out, this drink is hot!"];
    
    NSLog(@"%@", coffeeLabel)
    ```

##Properties vs Arguments

**Giant Object-Oriented design mistake: Passing in information about the state of an object to one of its methods** 

**Solution: Better to have properties so methods can access them using self**

ex: Changing DroidPhone method "reportBatteryLife:" to a property "batteryLife"

+ DroidPhone.h updates
    + add property ```batteryLife```
    + change reportBatteryLife into method that takes property ```self.batteryLife```, no arguments

        ```
        DroidPhone.h // OO-design mistake: method with arguments

        @interface Angel : NSObject

        @property NSString *phoneName;
        @property NSString *modelNumber;

        - (void) reportBatteryLife:(NSNumber *)battery;   
        - (NSString *) speak:(NSString *)greeting;

        @end

        ```

        ```
        DroidPhone.h //Correct: add property

        @interface Angel : NSObject

        @property NSString *phoneName;
        @property NSString *modelNumber;
        ** @property NSNumber *batteryLife; **

        ** - (void) reportBatteryLife ** 
        - (NSString *) speak:(NSString *)greeting;

        @end

        ```
+ DroidPhone.m updates
    + ```reportBatteryLife```method takes property ```self.batteryLife```
    + remove arguments
        
        ```   
        #import "DroidPhone.h"

        @implementation DroidPhone

        - (void) reportBatteryLife:(NSNumber *)battery;
        {
            NSLog(@"Battery life is %@", battery);
        }

        - (NSString *)speak:(NSString *)greeting;
        {
            NSString *message = [NSString stringWithFormat:@"%@ says %@", self.phoneName, greeting];
            return message;
        }
        @end
        ```
        
        ```
        #import "DroidPhone.h"

        @implementation DroidPhone
        - (void) reportBatteryLife;
        {
            NSLog(@"Battery life is %@", self.batteryLife);
        }
        - (NSString *) speak:(NSString *)greeting;
        {
          NSString *message = [NSString stringWithFormat:@"%@ says %@", self.phoneName, greeting];
          return message;
        }
        @end
        ```

##Properties: read-only

Prevent outside code from changing properties...

_Solutions_

1. make them *readonly*
    + set the ```readonly``` attribute to a property : ```@property (readonly) NSString *lastName;```
    + this means that code outside the class can no longer set the property. If they try, they will get an error ```Assignment to readonly property```
    + **However, even methods can't change readonly properties** : ```self.lastName``` = ```person.lastName```. Both treated as outside code.

2. **To get past ```readonly``` attribute / make changes internally**
    + ```_lastName = newLastName;```
    + Every property has a special *internal* variable that is prefixed with an underscore ```_```. This way a property can be read-only to the outside world, but methods on the class are able to update the property's value.
    
##Default property
Set default values to properties by taking advantage of a feature of inheritance: *method overriding*. For example, log every time a new ```Person``` object is created by overriding the ```init```method.

```
#import "Person.h"

@implementation Person
- (Person *) init;
{
    NSLog(@"Cool, a new Person is being initialized");
    
    return [super init];
}
@end
```

###Breakdown

+ the above ```init``` overrides the method defined in ```NSObject```, which ```Person``` inherits from.
+ ```init``` should return a ```Person *``` object but isn't returning anything so it needs another *special variable*: ```super```
+ ```super``` calls back up into the ```init``` method defined in ```NSObject```

**We're also able set *internal* variables on the current object being initialized before we return ```[super init]```.**

```
#import "Person.h"

@implementation Person
- (Person *) init;
{
    NSLog(@"Cool, a new Person is being initialized");
    _firstName = @"Tim";
    _lastName = @"Cook";
    return [super init];
}
@end
```
###Breakdown
+ Now every ```Person``` object created will start out with its firstName set to ```@"Tim"``` and lastName set to ```@"Cook"```

##Create instance variables

ex: ```Coffee``` class has a ```temperature``` property that we want to replace with an *instance variable*

+ Coffee.h with ```temperature``` property

```
Coffee.h        // with 'temperature' property

@interface Coffee : NSObject
@property NSNumber *temperature; 
@end
```

+ Coffee.h with ```temperature``` instance variable

```
Coffee.h        with 'temperature' instance variable
@interface Coffee : NSObject {
  NSNumber *_temperature;
}        
@end
```

###Breakdown
Instance variables:

+ go in optional curly-brace block after ```@interface``` declaration
+ defined like any other variable
+ keep naming convention for internal variables: ```_temperature```
