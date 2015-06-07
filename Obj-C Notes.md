#Objective-C Notes
##Etiquette
+ *Always* prefix strings with "**@**"
+ *Always* end declaration with "**;**"

##Basic Objects
###NSLog()
+ outputs whatever is between the () to the console
+ String interpolation : NSLog(@"Hello, %@, %@, %@", firstVar, secVar, thirdVar)
+ 

###NSString
+ Variable declaration for strings : NSString **variable* = @"blahblah";
+ 

###NSNumber
+ Variable declaration for numbers : NSNumber **variable* = @1234;
+ Log number object : NSLog(@"%@", variable);
    + Unlike string objects, you cannot log a NSNumber object by passing it directly to NSLog.
+ 
