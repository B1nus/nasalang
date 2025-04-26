# nasalang
My attempt at enforcing [Nasa's power of 10](https://code.with-madrid.com/en/latest/nasa10.html) in a language. It's a simpler language to let me go from idea to prototype quickly.

No recursive `use` calls.
Only sub folders in `use` calls.
Only one level of `use` calls.
Only `use` at start of file.
Maybe we can even forgo the `use` keyword (:

Return only at end of function.
Functions can only use parameters. no global variables.
Functions cannot mutate ther parameters. All arguments are copied.
No functions inside functions.
No empty function bodies.

No comments.

Automatic formatter which uses the ast. <- great way to test the ast
  Note: Ideally the formatter shouldn't be necessary. There should only be one way to write something which compiles.
Formatting:
indentation = two spaces
empty line between functions
no newline between statements
locals at the top of a function
one space between each token

Operators: `add sub mul div rem and or xor clz ctz popcnt eqz eq ne lt gt le ge shl shr rotl rotr abs neq sqrt ceil floor trunc nearest min max copysign extend wrap trunc demote promote convert reinterpret`

Builtins: `load_u8 load_u16 load_u32 load_u64 load_s8 load_s16 load_s32 load_s64 load_f32 load_f64 load_bool store_u8 store_u16 store_u32 store_u64 store_s8 store_s16 store_s32 store_s64 store_f32 store_f64 store_bool memory_copy memory_fill allocate`

Function: `"func" name ((indentation (name type)+ dedentation) | newline) "result" type* indentation statement* ("return" indentation (expression newline)+ dedentation)?`

Binding: `name type dedentation/newline`

Assignment: `name "=" expression dedentation/newline` or `name, name, name ... = name indentation (expression newline)* dedentation`

Types: `bool u8 u16 u32 u64 s8 s16 s32 s64 f32 f64`

Data: `hello_ptr, hello_len = "Hello!\00\00"`

Name: `name_n1234rt5y6ame_name12234567` snake case.

Stack:
Store the stack ptr at start of each scope (func, if, repeat) on the wasm stack. As each allocation increases the ptr. When the scope ends the next item on the stack should be the return pointer. So we just consume that then.

main
```
use
  utils
  math

func main
  args_ptr u32
  args_len u32
result s32
  index u32
  list_ptr u32
  index = find
    args_ptr
    args_len
    0
  list_ptr = array
    index
  drop array
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
