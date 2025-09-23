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

To make our mini-fuzzer program with libFuzzer, we need to make a  `fuzz target` [function](https://llvm.org/docs/LibFuzzer.html#fuzz-target)

* Note: Fuzzers main function is to generate inputs, its the programmers responsibility to detect the bugs from these inputs (ie. using sanitizers, gdb debugger etc)

### Using Fuzzers

* Suppose we want to link a fuzzer function to test another function

```
//fuzzer.c  file            | // func_f.c file
                            |
-> func_f header here       | test_func(num){    // say this function returns the abs val of num
                            |   ...
-> fuzz_func{               |   }
    .                       |
    .                       |
    call func_f(num)        |
}                           |

```

Command format to use fuzzer to generate inputs to test func_f:

`clang -sanitize=<sanitizer-flag to incorporate>, fuzzer -g <name of fuzzer file> <test_func file> -o output_file`

For A5 I use: 

`clang -sanitize=undefined, fuzzer -g fuzzer.c func_f.c -o test_func_with_myfuzzer`