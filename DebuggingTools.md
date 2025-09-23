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

* Resource: [libFuzzer](https://llvm.org/docs/LibFuzzer.html)

When we get a bug report from sanitizers, we can try to repeat this error => identify it => fix it.  But how do we know 
what value to pass?  

`Fuzzers` are input generators.  Think of it as a mini side program that keeps running to generate new inputs that will 
test the program we are working on by seeing if new generated inputs triggers any problems. `For example:` [Google's OSS Fuzz Project](https://github.com/google/oss-fuzz)