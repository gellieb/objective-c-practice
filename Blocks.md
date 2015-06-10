#Blocks
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

