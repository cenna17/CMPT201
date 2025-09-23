# Debugging Tools (Refernce Activity: A5)

## Logging && Assertions

* Logging is used to track a programs flow. `Most common /var/log` files store info that tracks the execution of the program 

* Assertions check T/F status of conditions; if false -> throw error.  We usually use it to `check input params and return values`. 

=> `Format: Assert(condit'n)` MUST INCLUDE `#include <assert.h>` TO USE ASSERTION FUNCTION

## Checkers -> Sanitizers 

* Sanitizers are like flags that we can ask the compiler to check for. 

* `clang -fsanitize=??? file.c -o output_file` is the format we use

=> `???` is the sanitizer flag that you want to enable

=> eg) `-fsanitize=undefined` gives more detailed error message when undefinedBehaviour error is detected in execution

### Static vs Dynamic Checkers

`Static Check` - Done at compile time; completed by reading & analyzing code rather than by running it.

`Dynamic Check` - Done at run time `<-` Sanitizers ar this group

## Fuzzers