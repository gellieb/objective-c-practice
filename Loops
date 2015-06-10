#Loops
##Simple if condition
```
BOOL meanieBoBeanie = [mrHiggie areYouMean];  //Setting object 'mrHiggie' to variable 'meanieBoBeanie' with method 'areYouMean' that returns a BOOL

if (meanieBoBeanie) {
    NSLog(@"Confirmed: this is true.");
} else {
    NSLog(@"Confirmed: you lie.")
}
```

+ ```BOOL``` : a special data type. A variable defined with ```BOOL``` type can be ```YES (true)```or ```NO (false)```

## Comparision with NSNumber
+ Must convert ```NSNumber``` to ```int``` with ```intValue```
+ ```[NSNumberVariable intValue] ``` // int type

```
NSNumber *meannessScale = [mrHiggie meannessScale]  // Just creating empty class of mrHiggie. meannessScale returns a NSNumber

if([meannessScale intValue] < 4) {                  // must convert NSNumber to int with intValue 
  NSLog(@"Mr. Higgie is on the nice side");
} else if([meannessScale intValue ]< 8) {
  NSLog(@"Mr. Higgie is sorta nice but not really");
} else {
  NSLog(@"Mr. Higgie is definitely mean");
}

```

##Equality
+ ```isEqualToString:``` compares two ```NSString``` objects

```
if([myString isEqualToString:otherString]) {        // BOOL -> YES or NO
  NSLog(@"Hello from inside the if!");
}
```
##Switch statements
+ Use a ```switch``` when a variable can be one of a limited set of values and different code needs to be executed based on the single variable

```
NSInteger day = getDayOfWeek();

switch (day) {
  case 1: {
    NSLog(@"Monday");
    break;
  }
  case 2: {
    NSLog(@"Tuesday");
    break;
  }
  /* snip Wednesday through Saturday */
  case 7: {
    NSLog(@"Sunday");
    break;
  }
}
```
    
+ **Use ```switch``` and ```enum```**
    + ```enum``` allows you to define a variable that can be only 1 of a limited set of values
    + Instead of: ```NSInteger day = 1;```, write ```DayOfWeek day = 1;```
        + ```DayOfWeek``` is just an *alias* for ```NSInteger```, not a whole new type
    + Cleaner and easier to read
+ **Define NS_ENUM**

```
typedef NS_ENUM(NSInteger, DayOfWeek) {             // Assign each day of the week corresponding the NSInteger value.
                                                    // Now we can use 'DayOfWeekWednesday' instead of '3' => More readable code. => Safer because Obj-C is smart enough to make sure all the possible values for 'DayOfWeek' are handled in the 'switch'
    DayOfWeekMonday = 1,
    DayOfWeekTuesday = 2,
    DayOfWeekWednesday = 3,
    DayOfWeekThursday = 4,
    DayOfWeekFriday = 5,
    DayOfWeekSaturday = 6,
    DayOfWeekSunday = 7
};
```
+ Switch

```
DayOfWeek day = getDayOfWeek();                     // Returns int value 1-7

switch (day) {
    case DayOfWeekMonday:
    case DayOfWeekTuesday:
    case DayOfWeekWednesday:
    case DayOfWeekThursday: {
        [mrHiggie setCurrentHat:@"Fedora"];
        break;
    }
    case DayOfWeekFriday: {
        [mrHiggie setCurrentHat:@"Sombrero"];
        break;
    }
    case DayOfWeekSaturday:
    case DayOfWeekSunday: {
        [mrHiggie setCurrentHat:@"AstronautHelmet"];
        break;
    }
}

NSLog(@"Mr. Higgie is wearing: %@", [mrHiggie currentHat]);
```

##Fast Enumeration / for(NSString *var in NSArrayObject)
```
NSArray *funnyWords = @[@"Schadenfreude", @"Portmanteau", @"Penultimate"];

for (NSString *word in funnyWords) {
  NSLog(@"%@ is a funny word", word);
}
```
_How it works_

+ Execute the code inside ```{}``` for each ```NSString``` in the ```funnyWords``` collection.

##Enumerating an NSDictionary
+ *Fast Enumeration* isn't limited to ```NSArray``` objects and can be used on ```NSDictionary``` objects too

```
NSDictionary *funnyWords = @{
  @"Schadenfreude": @"pleasure derived by someone from another person's misfortune.",
  @"Portmanteau": @"consisting of or combining two or more separable aspects or qualities",
  @"Penultimate": @"second to the last"
};

for (NSString *word in funnyWords){
  NSString *definition = funnyWords[word];
  NSLog(@"%@ is defined as %@", word, definition);
}
```
