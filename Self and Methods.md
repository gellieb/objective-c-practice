#Self and Methods
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
