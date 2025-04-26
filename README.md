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
1. No `goto` and no recursion. You can only call functions previously defined.
2. One `repeat` keyword which takes a positive integer argument.
3. No dynamic allocation.
4. Error on functions longer than 60 lines.
5. Error on less than two assertions per function on avarage.
6. No global scope. Error if the scope is unnecessarily large. Functions can only use their parameters.
7. `ignore` keyword to ignore return values.
8. No preprocessor. `use` keyword to include files.
9. No pointers, no function pointers.
10. All warnings are errors. And all errors stop compilation.

No recursive `use` calls.
Only sub folders in `use` calls.
Only one level of `use` calls.
Return only at end of function.

Automatic formatter.

main
```
use
  utils
  math

func main
  args_ptr u32
  args_len u32
result s32
  index = find
    args_ptr
    args_len
    0
  list_ptr = array
    index
  memory_copy
    list_ptr
    args_ptr
    index
  output
    list_ptr
    index
```
utils
```
func find
  ptr u32
  len u32
  byte u8
result u32
  index u32 = 0
  repeat len
    if load_u8(index + ptr) == byte
      break
    index = index + 1
  return index

func join
  ptr u32
  len u32
  other_ptr u32
  other_len u32
result u32 u32
  return
    0
    0
```
