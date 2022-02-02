# C basics

## Pointers

| Symbol + Use  | Term                                                                       | Description                                                         |
| ------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `int *p = 5;` | pointer, "p"                                                               | _declare_ the pointer-variable, p, and assign a value of 5.         |
| `*p`          | <ul><li>indirection operator</li><li>dereference the pointer<br></li></ul> | Change or access/ reference the value that pointer p is pointing to |
| `p = &x;`     | assign to address-of                                                       | assign (point) p to address space containing value of variable x    |

## Language and Environment

* Two types of _execution environments:_&#x20;
  * _freestanding:_ A programming environment where typically no OS is provided. Used primarily for programming on embedded systems.&#x20;
  * _hosted:_ a "friendlier" programming environment with standard libraries, OS, memory management, etc.&#x20;
* "C is a <mark style="color:purple;">call-by-value</mark> (also called a pass-by-value) language, which means that when you provide an argument to a function, the value of that argument is copied into a distinct variable for use within the function."

## References

* Effective C: An Introduction to Professional C Programming, Robert C. Seacord
* [Code Vault, YouTube](https://www.youtube.com/c/CodeVault/videos)
* [Caleb Curry, YouTube](https://youtube.com/playlist?list=PL\_c9BZzLwBRKKqOc9TJz1pP0ASrxLMtp2)
