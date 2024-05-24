


## POINTER funamentals
<https://www.geeksforgeeks.org/pointers-in-golang/>
<https://medium.com/@jamal.kaksouri/a-comprehensive-guide-to-pointers-in-go-4acc58eb1f4d>


difference between pointer receiver and value reveiver

```
Pointer Receiver:
func (tc *TestCase) Validate() error {
}


Value Receiver:
func (tc TestCase) Validate() error {
}
```


### * and &

In Go, & and * are operators used for working with pointers, which are fundamental to Go's memory management and are widely used in various programming scenarios.

& (Address Operator): The & operator is used to get the memory address of a variable. When you use & followed by a variable name, it returns the memory address where that variable is stored in the computer's memory. For example:

```go
x := 42
fmt.Println(&x) // This will print the memory address of variable x
```

* (Dereference Operator): The *operator is used to access the value stored at a memory address, i.e., it dereferences a pointer. When you have a pointer to a variable and you want to access the actual value stored at that memory location, you use*. For example:

```go
x := 42
ptr := &x    // ptr is now a pointer to the memory address of x
fmt.Println(*ptr) // This will print the value stored at the memory address ptr points to, which is 42
```

Combining & and * allows you to work with pointers effectively. Here's a simple example that demonstrates their use together:

```go
package main

import "fmt"

func main() {
    x := 42
    fmt.Println("Value of x:", x)        // Prints the value of x
    fmt.Println("Memory address of x:", &x) // Prints the memory address of x

    ptr := &x
    fmt.Println("Value at pointer:", *ptr)  // Prints the value at the memory address ptr points to

    *ptr = 100   // Assigns 100 to the memory location pointed by ptr, which also changes the value of x
    fmt.Println("New value of x:", x)     // Prints the updated value of x
}
```

### defer, panic and recover

* <https://go.dev/blog/defer-panic-and-recover>
* <https://hussachai.medium.com/error-handling-in-go-a-quick-opinionated-guide-9199dd7c7f76>
