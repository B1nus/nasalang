Nasa power of 10:
1. No goto or recursion
2. Only limited loops
3. Only stack memory
4. Restrict functions to a single page
5. Minimum of two assertions per function
6. Restrict the scope of data to the smallest possible.
7. Explicit ignoring of return values
8. Limited use of the preprocessor
9. Limit pointer use to a single dereference, and do not use function pointers
10. All warnings should be address before releasing.

How my language interpretes these requirements:
1. No `goto` and no [recursion](https://softwareengineering.stackexchange.com/a/441475).
2. One `repeat` keyword which takes a positive integer argument.
3. Only arrays. `array 100 u8`
4. Error on functions longer than 60 lines.
5. Error on less than two assertions per function on avarage.
6. No global scope. Error if the scope is unnecessarily large. Functions can only use their parameters.
7. `ignore` keyword to ignore return values.
8. No preprocessor. `use` keyword to include files.
9. Error on more than one level of reference. No function pointers.
10. All warnings are errors. And all errors stop compilation.
