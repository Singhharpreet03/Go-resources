# Getting started with GO
# Resources
- [KodeKloud Go notes](https://notes.kodekloud.com/docs/Golang/Getting-Started/Course-Introduction)
- geek for geeks docs
- w3school


## Basic information
- every executable program writtne in go must contain main package and the man function is the entry point of the program.
- basic package "fmt" is used to print string and output
- it os fast and statically typed, compilied language

## Comments
```go
// this is single line comment

/*
multi line comments
*/
```

## printing hello world

```go
package main
import "fmt"

func main() {
  fmt.Println("Hello World!")
}

```


## Data types in Go

> short hand way of storing variables
> ```go
> var i,j string = "Hello","World" // if same data type
> // if different data types
> var ( 
>  i string = "hello" 
>  j int = 123
>)
>
>```

### String 
> size of string is 16 bytes
```go
var txt1 string = "Hello!"
txt3 := "World 1"
```

### Integer

The integer data type has two categories:

* Signed integers - can store both positive and negative values
* Unsigned integers - can only store non-negative values

> The default type for integer is int. If you do not specify a type, the type will be int.

```go
var x int = 500
var y int = -4500
var a uint = 500
var b uint = 4500
```

### Unsigned Integer Types  

| Type   | Size                  | Range                         |
|--------|-----------------------|------------------------------|
| uint   | 32 or 64 bits         | 0 to 4.29 billion (32-bit), 0 to 18.44 quintillion (64-bit) |
| uint8  | 8 bits / 1 byte       | 0 to 255                     |
| uint16 | 16 bits / 2 bytes     | 0 to 65,535                  |
| uint32 | 32 bits / 4 bytes     | 0 to 4.29 billion            |
| uint64 | 64 bits / 8 bytes     | 0 to 18.44 quintillion       |

### Signed Integer Types  

| Type   | Size                  | Range                         |
|--------|-----------------------|------------------------------|
| int    | 32 or 64 bits         | -2.14 billion to 2.14 billion (32-bit), -9.22 quintillion to 9.22 quintillion (64-bit) |
| int8   | 8 bits / 1 byte       | -128 to 127                  |
| int16  | 16 bits / 2 bytes     | -32,768 to 32,767            |
| int32  | 32 bits / 4 bytes     | -2.14 billion to 2.14 billion |
| int64  | 64 bits / 8 bytes     | -9.22 quintillion to 9.22 quintillion |

### Special Integer Types in Go  

| Type    | Description |
|---------|------------|
| **rune**   | A synonym for `int32`, used to represent Unicode code points. |
| **byte**   | A synonym for `uint8`, often used for raw byte data. |
| **uintptr** | An unsigned integer type that can hold all the bits of a pointer value. Its width depends on the platform. |


### Floating point

> The default type for float is float64. If you do not specify a type, the type will be float64.

```go
var x float32 = 123.78
var y float32 = 3.4e+38
var x float64 = 1.7e+308
```

### Floating-Point Types

| Type    | Size     | Range                        |
|---------|---------|-----------------------------|
| float32 | 32 bits | -3.4e+38 to 3.4e+38         |
| float64 | 64 bits | -1.7e+308 to 1.7e+308       |


### Boolean
> size of boolean is 1 byte of memory
```go
var b1 bool = true // typed declaration with initial value
var b2 = true // untyped declaration with initial value
var b3 bool // typed declaration without initial value
b4 := true // untyped declaration with initial value
```
### Array 
collection of same data type
- Fixed-size collection of elements of the same type.  
- Declared with a specific length (`[size]Type`).  
- Default values are zero (`0` for numbers, `""` for strings).  
- Cannot be resized after declaration.  
  
```go
package main

import "fmt"

func main() {
    // Standard declaration
    var arr1 [3]int = [3]int{1, 2, 3}

    // Shorthand declaration
    arr2 := [3]int{4, 5, 6}

    // Let Go determine the size
    arr3 := [...]int{7, 8, 9}

    fmt.Println(arr1) // [1 2 3]
    fmt.Println(arr2) // [4 5 6]
    fmt.Println(arr3) // [7 8 9]
}
```

### slices   
A slice consists of three key components:

- Pointer: Refers to the first accessible element in the underlying array (which may not be the first element of the entire array).
- Length: The number of elements contained in the slice.
- Capacity: The total number of elements in the underlying array starting from the first element in the slice.


- **Dynamic** size, unlike arrays.  
- Internally backed by an **array** but can grow/shrink.  
- **Reference type**, modifying a slice affects the underlying array.  

### **Ways to Initialize Slices:**  
- **Shorthand:** `s := []int{1, 2, 3}`  
- **From an array:** `s := arr[1:3] // From index 1 to 2`  
- **Using `make([]datatype,length,capacity)`:**  
  - With length: `s := make([]int, 3) // Length = 3, capacity = 3`  
  - With length & capacity: `s := make([]int, 3, 5) // Length = 3, capacity = 5`  

## `append()` Function in Go  

- Adds elements to a **slice** dynamically.  
- If capacity is exceeded, a **new array is allocated** with **double** the capacity.  

### **Syntax:**  
- **Basic:** `s = append(s, 4, 5)`  
- **Appending another slice:** `s = append(s, t...)`  

### **Example:**  
```go
s := make([]int, 2, 3) // len=2, cap=3
s = append(s, 10, 20)  // New array allocated (cap doubles)
```
### copy fuunction

- Go provides a built-in copy function to copy elements from one slice to another. 
- This function returns the number of elements that were successfully copied, which is the minimum of the lengths of the source and destination slices
> both of the slices must of same data type
```go
// Syntax:
func copy(dst, src []Type) int
// Example:
num := copy(dest_slice, src_slice)
```
```go
package main

import "fmt"

func main() {
    src_slice := []int{10, 20, 30, 40, 50}
    dest_slice := make([]int, 3)  // Destination slice with length and capacity 3
    num := copy(dest_slice, src_slice)
    fmt.Println(dest_slice)
    fmt.Println("Number of elements copied:", num)
}
```
### map 
  
- **Key-value pairs** for fast lookups.  
- **Keys must be unique** and of a comparable type.  
- **Unordered**, no guaranteed order of iteration.  
- It's important to note that indexing a map in Go returns two values: the value itself and a boolean indicating whether the key exists. The syntax is: `value, found := map_name[key]`
### **Ways to Initialize Maps:**  
- **Using `make()`:** `m := make(map[string]int)`  
- **standard initilaisation** `var my_map map[string]int`
> This syntax initializes a nil map. The zero value of a map in Go is nil, meaning it doesn't contain any keys. Trying to add a key-value pair to a nil map will result in a runtime error.
- **Shorthand declaration:** `m := map[string]int{"a": 1, "b": 2}`  

### **Basic Operations Map:**  
- **Add/Update:** `m["key"] = value`  
- **Retrieve:** `val := m["key"]`  
- **Delete key:** `delete(m, "key")`  
- **Check existence:** `val, exists := m["key"]` 


## printing variables 

string

```go
var name string = "hp"
var city string = "gzb"

fmt.Print("welcome ",name,", ",city)
fmt.Println("welcome ",name,", ",city)
```

### printf - format specifier

```go
var i string = "Hello"
var j int = 15

fmt.Printf("i has value: %v and type: %T\n", i, i)

fmt.Printf("j has value: %v and type: %T", j, j)
fmt.Printf("j has value: %d and type: %T\n", j, j)

```
### Format Specifiers in Go

| Specifier | Description |
|-----------|-------------|
| **General Formatting** | |
| `%v`  | Default format for the value |
| `%+v` | Adds field names for structs |
| `%#v` | Go syntax representation of the value |
| `%T`  | Type of the value |
| `%%`  | A literal percent sign `%` |
| **Boolean Formatting** | |
| `%t`  | Boolean (`true` or `false`) |
| **Integer Formatting** | |
| `%b`  | Binary representation |
| `%c`  | Character representation (corresponding Unicode code point) |
| `%d`  | Decimal representation |
| `%o`  | Octal representation |
| `%O`  | Octal with `0o` prefix |
| `%q`  | Single-quoted character literal |
| `%x`  | Hexadecimal (lowercase) |
| `%X`  | Hexadecimal (uppercase) |
| `%U`  | Unicode format (`U+hhhh`) |
| **Floating-Point & Complex Numbers** | |
| `%b`  | Scientific notation with exponent as power of two |
| `%e`  | Scientific notation (`e` notation, lowercase) |
| `%E`  | Scientific notation (`E` notation, uppercase) |
| `%f`  | Decimal representation (no exponent) |
| `%F`  | Equivalent to `%f` |
| `%g`  | Uses `%e` or `%f` (whichever is shorter) |
| `%G`  | Uses `%E` or `%F` (whichever is shorter) |
| **String & Slice of Bytes Formatting** | |
| `%s`  | Plain string |
| `%q`  | Double-quoted string with Go syntax escape sequences |
| `%x`  | Hexadecimal encoding (lowercase) |
| `%X`  | Hexadecimal encoding (uppercase) |
| **Pointer Formatting** | |
| `%p`  | Pointer address in hexadecimal |

## `var` vs `:=` in Go

| Feature | `var` | `:=` |
|---------|------|------|
| Scope | Can be used inside and outside of functions | Can only be used inside functions |
| Declaration & Assignment | Can be done separately | Must be done in the same line |

### Zero Values of Data Types in Go

| Data Type  | Zero Value |
|------------|-----------|
| `int`      | `0`       |
| `float32`  | `0.0`     |
| `float64`  | `0.0`     |
| `bool`     | `false`   |
| `string`   | `""` (empty string) |
| `rune`     | `0` (represents the null character) |
| `byte`     | `0`       |
| `pointer`  | `nil`     |
| `slice`    | `nil`     |
| `map`      | `nil`     |
| `channel`  | `nil`     |
| `interface{}` | `nil`     |
| `function` | `nil`     |

In Go, all variables are initialized with their respective zero values if not explicitly assigned.

## Taking Input in Go

In Go, you can take user input using the `fmt`, `bufio`, and `os` packages.

### Using `fmt.Scan`
Reads space-separated values from standard input.

```go
package main

import "fmt"

func main() {
    var name string
    fmt.Print("Enter your name: ")
    fmt.Scan(&name)
    fmt.Println("Hello,", name)
}
```
### Using `fmt.Scanf`
Allows formatted input.

```go
package main

import "fmt"

func main() {
    var age int
    fmt.Print("Enter your age: ")
    fmt.Scanf("%d", &age)
    fmt.Println("Your age is", age)
}
```
### Using `bufio.NewReader`
For reading a full line (including spaces), use bufio.NewReader.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    reader := bufio.NewReader(os.Stdin)
    fmt.Print("Enter your full name: ")
    name, _ := reader.ReadString('\n')
    fmt.Println("Hello,", name)
}
```
### Using `os.Stdin`
To read raw input data:
```go
package main

import (
    "fmt"
    "io"
    "os"
)

func main() {
    data, _ := io.ReadAll(os.Stdin)
    fmt.Println("Input received:", string(data))
}
```
## `fmt.Scanf` Return Types in Go

The `fmt.Scanf` function returns two values:

1. **Count (int)**: The number of successfully scanned items.
2. **Error (error)**: An error if scanning fails, otherwise `nil`.

### Example: Using `fmt.Scanf` with Return Values

```go
package main

import "fmt"

func main() {
    var age int
    var name string

    fmt.Print("Enter your name and age: ")
    count, err := fmt.Scanf("%s %d", &name, &age)

    fmt.Println("Error: ", err)
    fmt.Println("Count: ", count)
    fmt.Println("name: ", name)
    fmt.Println("age: ", age)
}
```
## Checking Variable Type in Go  
- Use `%T` with `fmt.Printf`: `fmt.Printf("%T", x)` prints the type.  
- Use `reflect.TypeOf`: `fmt.Println(reflect.TypeOf(x))` returns the type.  

## Type Casting in Go  

- **int to float**: `float64(x)` converts `int` to `float64`.  
- **float to int**: `int(x)` truncates the decimal part.  

## String Conversion (`strconv` Package)  

- **`strconv.Itoa(x)`** → Converts `int` to `string`.  
- **`strconv.Atoi(s)`** → Converts `string` to `int`. Returns `(int, error)`.  

## `const` in Go  

- Constants are immutable values.  
- Can be **typed** or **untyped**.  
- need to declare at the time of intialisation or else will get an error missing declaration
- no concept of zero value
- no short hand assignment (:=)

### **Untyped vs Typed Constants**  

| Type   | Description | Example |
|--------|------------|---------|
| **Untyped** | Value without a fixed type, adapts based on usage. | `const x = 10` (Can be `int`, `float`, etc.) |
| **Typed**   | Has a fixed type, cannot change. | `const y int = 10` (Always `int`) |

### **Example**  
```go
const a,b = 42, "hello"     // Untyped  
const b int = 42 // Typed  
```

## Operator Categories in Go  

- **Comparison Operators** → `==`, `!=`, `>`, `<`, `>=`, `<=` (return `bool`).  
- **Arithmetic Operators** → Perform math operations (`+`, `-`, `*`, `/`, `%`). 
> addition (+) also supports string concatenation. 

> when using the division operator with integers, Golang performs integer division, which may truncate any fractional part.
- **Assignment Operators** → Assign values, often with arithmetic (`=`, `+=`, `-=`, `*=`, `/=`, `%=`).  
- **Bitwise Operators** → Work on binary data (`&`, `|`, `^`, `&^`, `<<`, `>>`).  
- **Logical Operators** → Combine boolean conditions (`&&`, `||`, `!`).  

## If-else if-else

> Remember to always place the else on the same line as the closing brace to prevent syntax errors in Go.

```go
package main
import "fmt"


func main() {
    var fruit string = "grapes"
    if fruit == "apples" {
        fmt.Println("Fruit is apple")
    } else {
        fmt.Println("Fruit is not apple")
    }
}
```

```go
package main


import "fmt"


func main() {
    fruit := "grapes"
    if fruit == "apple" {
        fmt.Println("I love apples")
    } else if fruit == "orange" {
        fmt.Println("Oranges are not apples")
    } else {
        fmt.Println("no appetite")
    }
}
```

## Switch statement

it uses implicit break statement so only the first matcing case works

```go
package main
import "fmt"


func main() {
    var i int = 800
    switch i {
    case 10:
        fmt.Println("i is 10")
    case 100, 200:
        fmt.Println("i is either 100 or 200")
    default:
        fmt.Println("i is neither 0, 100 or 200")
    }
}
```
### fallthrough keyword
`fallthrough` 

An interesting feature of Go's switch statement is the use of the fallthrough keyword. This keyword forces the execution to continue into the next case block, regardless of whether that subsequent case matches the switch expression.
```go
package main
import "fmt"


func main() {
    var i int = 10
    switch i {
    case -5:
        fmt.Println("-5")
    case 10:
        fmt.Println("10")
        fallthrough
    case 20:
        fmt.Println("20")
        fallthrough
    default:
        fmt.Println("default")
    }
}
```
output:
```go
10
20
default
```

## For loop

```go
for i := 1; i <= 3; i++ {
    fmt.Println("Hello World")
}
```
- `break` - break the current loop
- `continue` - skip the current iteration to next 


## `len()` Function in Go  

- **Arrays:** `len([5]int{10, 20, 30, 40, 50}) // 5`  
- **Slices:** `len([]int{1, 2, 3}) // 3`  
- **Strings:** `len("Hello") // 5`  
- **Maps:** `len(map[string]int{"a": 1, "b": 2}) // 2`  
## `cap()` Function in Go  

- Returns the **capacity** of a slice.  
- **Example:** `cap(make([]int, 3, 5)) // 5`  
- for array capacity and length are same

## Blank Identifier (`_`) in Go  

- **Used to ignore values** from functions.  
- **Prevents unused variable errors.**  
- **Commonly used** for ignoring return values.  

### **Example Blank identifier:**  
```go
value, _ := someFunction() // Ignoring the second return value
```

## `range` Function in Go  

- Used to iterate over arrays, slices, maps, and strings.  
- Returns **index & value** for slices/arrays, **key & value** for maps.  

### **Example Usage of range:**  
```go
for index, value := range []int{10, 20, 30} {
    fmt.Println(index, value) // 0 10, 1 20, 2 30
}
```

## Functions 

In Go, function names must adhere to specific naming rules:

- They must begin with a letter or an underscore.
- They can include additional letters, digits, and underscores.
- They are case sensitive.
- They cannot contain spaces.



```go
package main
import "fmt"


func operation(a int, b int) (int, int) {
    sum := a + b
    diff := a - b
    return sum, diff
}


func main() {
    sum, difference := operation(20, 10)
    fmt.Println(sum, difference)
}
```

## Named Return Parameters in Go  

- Allows naming return values in the **function signature**.  
- Enables **implicit return**, making code cleaner.  

### **Example:**  
```go
package main
import "fmt"

func operation(a int, b int) (sum int, diff int) {
    sum = a + b
    diff = a - b
    return // Implicitly returns sum and diff
}

func main() {
    sum, difference := operation(20, 10)
    fmt.Println(sum, difference) // Output: 30 10
}
```
> Named return parameters hold default zero values if not explicitly set.
Useful for functions with multiple return values, improving readability.

## Variadic Functions in Go  

- Accept a **variable number of arguments** using `...`.  
- The variadic parameter behaves like a **slice** inside the function.  
- **Must be the last parameter** in the function signature.  

### **Syntax:**  
```go
func functionName(param1 type, param2 ...type) returnType
```
Example
```go
func sumNumbers(numbers ...int) int {
    sum := 0
    for _, value := range numbers {
        sum += value
    }
    return sum
}

func main() {
    fmt.Println(sumNumbers(10, 20, 30)) // Output: 60
}
```

## Anonymous Functions in Go  

- **Functions without a name**, used for short-lived operations.  
- **Useful for encapsulating logic** without polluting the global namespace.  
- **Can be assigned to variables** or **invoked immediately.**  

### **Example 1: Assigned to a Variable**  
```go
x := func(a int, b int) int {
    return a * b
}
fmt.Println(x(20, 30)) // Output: 600
```
### invoke after declaration
```go
x := func(a int, b int) int {
    return a * b
}(20, 30)
fmt.Println(x) // Output: 600

```

## High order functions

Functions that either accept another function as an argument or return a function as output. High-order functions enable modular composition, allowing you to build complex operations from small, focused functions

Example 
```go
func printResult(radius float64, calcFunction func(r float64) float64) {
	result := calcFunction(radius)
	fmt.Println("Result: ", result)
	fmt.Println("Thank you!")
}

func getFunction(query int) func(r float64) float64 {
	queryToFunc := map[int]func(r float64) float64{
		1: calcArea,
		2: calcPerimeter,
		3: calcDiameter,
	}
	return queryToFunc[query]
}

func main() {
	var query int
	var radius float64


	fmt.Print("Enter the radius of the circle: ")
	fmt.Scanf("%f", &radius)
	fmt.Printf("Enter \n 1 - area \n 2 - perimeter \n 3 - diameter: ")
	fmt.Scanf("%d", &query)


	printResult(radius, getFunction(query))
}
```


## Defer Function in Go  

- **Delays execution** of a function until the surrounding function returns.  
- **Executed in LIFO (Last-In-First-Out) order** if multiple `defer` statements are used.  

### **Example:**  
```go
package main  
import "fmt"  

func main() {  
    defer fmt.Println("World")  
    fmt.Println("Hello")  
}  
// Output:  
// Hello  
// World  
```
# Pointers

A pointer holds the memory address of a variable. In Go, you can declare a pointer using the following syntax:

> uninitialized pointers in Go have the nil value.
```go
var <pointer_name> *<data_type>
var <pointer_name> *<data_type> = &<variable_name>
var <pointer_name> = &<variable_name>
<pointer_name> := &<variable_name>
```

## Derefencing an pointer
> By placing the dereference operator (an asterisk) before a pointer, you gain access to the value stored in the pointer’s referenced memory location. Moreover, you can modify the value by using the dereference operator in an assignment.
```go
*<pointer_name>
*<pointer_name> = <new_value>
```

```go
package main
import "fmt"


func main() {
    s := "hello"
    fmt.Printf("%T %v\n", s, s)
    ps := &s
    *ps = "world"
    fmt.Printf("%T %v\n", s, s)
}
```
# passing variable by refernce

```go
package main
import "fmt"

func modify(s *string) {
	*s = "world"
}

func main() {
	a := "hello"
	fmt.Println(a)
	modify(&a)
	fmt.Println(a)
}
```

> slices and maps are passed as refernce as default
```go
package main
import "fmt"

func modify(s []int) {
	s[0] = 100
}
func main() {
	slice := []int{10, 20, 30}
	fmt.Println(slice)
	modify(slice)
	fmt.Println(slice)
}
```
```go
package main
import "fmt"

func modify(m map[string]int) {
	m["K"] = 75
}

func main() {
	ascii_codes := make(map[string]int)
	ascii_codes["A"] = 65
	ascii_codes["F"] = 70
	fmt.Println(ascii_codes)
	modify(ascii_codes)
	fmt.Println(ascii_codes)
}
```

# Struct

A struct is a user-defined data type that groups together related data elements

## Declaring a Struct

```go
type <struct_name> struct {
    // list of fields
}
```
example
```go
type Student struct {
    name   string
    rollNo int
    marks  []int
    grades map[string]int
}
```
>No values are assigned during declaration, so each field is set to its default value (for example, zero for integers and an empty string for strings) until explicitly initialized.

## Initializing a struct
> **`%+v` is used to print all fields inside the struct using `fmt` package**
1. using `var` keyword
```go
package main
import "fmt"
type Student struct {
    name   string
    rollNo int
    marks  []int
    grades map[string]int
}
func main() {
    var s Student
    fmt.Printf("%+v", s)
}
```
> {name: rollNo:0 marks:[] grades:map[]}

2. Using `new` keyword
> it creates a pointer to the struct
```go
package main
import "fmt"
type Student struct {
    name   string
    rollNo int
    marks  []int
    grades map[string]int
}

func main() {
    st := new(Student)
    fmt.Printf("%+v", st) // st is a pointer to Student
}
```
3. with a Struct Literal using Field Names

```go
package main
import "fmt"
type Student struct {
    name   string
    rollNo int
}
func main() {
    st := Student{
        name:   "Joe",
        rollNo: 12,
    }
    fmt.Printf("%+v", st)
}
```

4. with a Struct Literal Without Field Names
```go
package main
import "fmt"
type Student struct {
    name   string
    rollNo int
}

func main() {
    st := Student{"Joe", 12}
    fmt.Printf("%+v", st)
}
```

## Accessing fields

```go
package main
import "fmt"
type Circle struct {
    x int
    y int
    radius int
}

func main() {
    var c Circle
    c.x = 5
    c.y = 5
    c.radius = 5
    fmt.Printf("%+v \n", c)
}
```
## passing structs to functions
> Passing by value means that modifications made inside the function do not alter the original struct. This is useful when you want to ensure the integrity of the initial data.

```go
package main
import "fmt"

type Circle struct {
    x      int
    y      int
    radius float64
    area   float64
}

func calcArea(c *Circle) {
    const PI float64 = 3.14
    var area float64
    area = PI * c.radius * c.radius
    (*c).area = area
}

func main() {
    c := Circle{x: 5, y: 5, radius: 5, area: 0}
    fmt.Printf("%+v \n", c)
    // Passing the address of 'c' so that modifications affect the original variable.
    calcArea(&c)
    fmt.Printf("%+v \n", c)
}
```
## Comparing Structs

- Struct equality operators (== and !=) can only be utilized if both operands are of the same type.
- Comparing structs of different types will result in a compile-time error.
- When comparing structs of the same type, all corresponding fields must hold equal values for the structs to be considered equal.

# Go Methods

## Method Syntax
A method in Go is like a function but has a **receiver parameter** (the instance it operates on):

```go
func (<receiver>) <method_name>(<params>) <return> {
    // code
}
```

## Pointer vs. Value Receivers
- **Pointer Receiver (`*T`)**: Modifies the original struct.
- **Value Receiver (`T`)**: Works on a copy, leaving the original unchanged.

### Example: Pointer Receiver (Modifies Struct)
```go
func (c *Circle) calcArea() { c.area = 3.14 * c.radius * c.radius }
```
```go
c := Circle{radius: 5}
c.calcArea()
fmt.Printf("%+v\n", c)  // {radius:5 area:78.5}
```

### Example: Value Receiver (No Modification)
```go
func (c Circle) calcArea() { c.area = 3.14 * c.radius * c.radius }
```
```go
c := Circle{radius: 5}
c.calcArea()
fmt.Printf("%+v\n", c)  // {radius:5 area:0}
```

## Key Takeaway
- Use **pointer receivers** when modifying the struct.
- Use **value receivers** for read-only operations.
# Go Method Sets

## What are Method Sets?
Method sets define the collection of methods associated with a type, allowing encapsulation and behavior definition.

## Example: `Student` Struct
```go
// Student structure with name and grades
 type Student struct {
    name   string
    grades []int
 }

// Method to display student name (Pointer Receiver)
func (s *Student) displayName() { fmt.Println(s.name) }

// Method to calculate average grade
func (s *Student) calculatePercentage() float64 {
    sum := 0
    for _, grade := range s.grades { sum += grade }
    return float64(sum) / float64(len(s.grades))
}
```

## Using Methods in `main()`
```go
func main() {
    s := Student{name: "Joe", grades: []int{90, 75, 80}}
    s.displayName()
    fmt.Printf("%.2f%%", s.calculatePercentage())
}
```
**Expected Output:**
```
Joe
81.67%
```

## Key Takeaway
- **Method sets** help define behaviors for custom types.
- **Essential for understanding interfaces in Go.**

# Go Interfaces: Introduction & Implementation

## What are Interfaces?
Interfaces define a set of method signatures without implementations, allowing flexible and decoupled code design.

## Defining an Interface
```go
type FixedDeposit interface {
    getRateOfInterest() float64
    calcReturn() float64
}
```
- **`getRateOfInterest()`** → Returns interest rate.
- **`calcReturn()`** → Computes the return.

## Implicit Implementation
A struct implements an interface **implicitly** by defining all required methods:

```go
type BankFD struct {
    rate float64
}

func (b BankFD) getRateOfInterest() float64 { return b.rate }
func (b BankFD) calcReturn() float64 { return b.rate * 1000 }
```

## Implementing Interfaces
### Defining the Interface
```go
type shape interface {
    area() float64
    perimeter() float64
}
```
- Any type implementing `area()` and `perimeter()` conforms to `shape`.

### Implementing the Interface with a Square
```go
type square struct {
    side float64
}

func (s square) area() float64 { return s.side * s.side }
func (s square) perimeter() float64 { return 4 * s.side }
```

### Implementing the Interface with a Rectangle
```go
type rect struct {
    length, breadth float64
}

func (r rect) area() float64 { return r.length * r.breadth }
func (r rect) perimeter() float64 { return 2*r.length + 2*r.breadth }
```

### Using the Interface
```go
func printData(s shape) {
    fmt.Println(s.area())
    fmt.Println(s.perimeter())
}

func main() {
    r := rect{length: 3, breadth: 4}
    c := square{side: 5}

    printData(r)
    printData(c)
}
```

## Key Takeaways
- Interfaces in Go **do not require explicit implementation**.
- They enable **modular and decoupled** code.
- Types implement interfaces **implicitly** by defining matching method signatures.
- A single function can operate on multiple types that share the same interface, increasing flexibility.
