# Syntax

## Assignment

## `for` Loop

The C-style `for` loop without parentheses:

    for initialization; condition; post {
        // zero or more statements
    }

- initialization: simple statement (variable declaration, function call)
- condition: expression returning a boolean value
- post: statement to be executed after every iteration

If initialization and post statement are omitted, it resembles a traditional
`while` loop:

    for condition {
        // zero or more statements
    }

The condition can be left away to create an infinite loop:

    for {
        // zero or more statements
        // break or return to end the loop
    }

### `for`/`range` loop

Looping over a slice, the `range` keyword produces a pair of variables, index
and value:

    for i, v := range s {
        // s[i] == v
    }

Looping over a map, `range` returns a key-value pair:

   for k, v := range m {
        // m[k] == v
   }

The values returned by `range` can also be omitted, looping len(s) times
without caring about the individual values of the slice:

    for range s {
        // do something
    }

## Increment/Decrement

The increment and decrement operators are short forms of adding/subtracting
one:

    a := 0

    a += 1 # 1
    a++ # 2

    a -= 1 # 1
    a-- # 0

The increment and decrement operators are statements, not expressions:

    i := 1
    j := 2
    i = j++ # illegal!

There is only a suffix but no prefix form:

    i := 0
    i++
    i--
    ++i # illegal!
    --i # illegal!

## `len` Function

Return the length of a slice or map:

    s := []string{"foo", "bar", "baz"}
    len(s) // 3

    m := map[string]int{"a": 1, "b", 2, "c", 3}
    len(m) // 3

## Slicing

Access an individual item `i` in a slice `s`:

    s[i]

Access a subsequence from `m` (inclusive) to `n` (exclusive) in a slice `s`:

    s[m:n] # elements m to n-1

The size of the resulting slice is `n-m`.

Get the length of the slice `s`:

    len(s)

Lower boundaries default to zero if missing:

    s[:n] # elements 0 to n-1

Upper boundaries default to `len(s)` if missing:

    s[m:] # elements m to len(s)-1

If both boundaries are omitted, the colon can be omitted, too:

    s[:] # elements 0 to len(s)-1
    s # same as above

## Blank Identifier `_`

If a returned variable is not of interest, and since unused variables cause a
compilation error, it can be discarded using the blank identifier `_`:

    err, val := foo.Bar()
    _, val := foo.Bar()
    err, _ := foo.Bar()

## String Concatenation

The `+` operator concatenates two strings:

    a := "foo"
    b := "bar"
    c := a + b // "foobar"

String concatenation can be combined with an assignment operator:

    a := "foo"
    a += "bar" # "foobar"

## Variable Declaration

There are four ways of declaring a variable:

1. `s := ""`
    - shortest and most used form
    - only within functions
    - to be used when the initial value is important
2. `var s string`
    - commonly used
    - relies on default initialization
    - also allowed outside of functions
    - to be used when the initial value is _not_ important
3. var s = ""
    - used for declaration of multiple variables
4. var s string = ""
    - redundant type/value declaration
    - useful if default value of a type an initialization value differ

Option 1 and 2 are generally prefered.

### Initialization

Variables default to a zero value, defined by its type:

    var i int       // 0
    var f float32   // 0.0
    var s string    // ""

The elements of compund types also default to zero:

    zeroes := make([]int, 3)
    fmt.Println(zeroes[0], zeroes[1], zeroes[2]) // 0 0 0

### Multiple Declarations

Multiple variables can be declared with one `var` statement:

    var a, b, c int

### Tuple Assignment

Multiple variables can be declared and assigned a value:

    a, b, c := 1, 2, 3

### The `new` Function

Variables of any type can be declared using the `new` function:

    i := new(int)
    f := new(float32)
    s := new(string)

The `new` function returns a pointer:

    fmt.Println(i, f, s) // prints addresses
    fmt.Println(*i, *f, *s) // prints values

## Package Declaration

Declare the package name on the top of a file:

    package main

## Package Imports

Import a single package:

    import "fmt"

Import multiple packages:

    import (
        "fmt"
        "os"
        "strings"
    )

## Functions

TODO

### Function Literal

A function literal can stand wherever a function reference can. Thus this code:

    func handler(w http.ResponseWriter, r *http.Request) {
        // ...
    }
    http.HandleFunc("/", handler)

Can be rewritten as:

    http.HandleFunc("/", func (w http.ResponseWriter, r *http.Request) {
        // ... 
    })

Such a function is called -- for its lack of a name -- a anonymous function.

## `make`

The `make` builtin function is used to build data structures, such as a `map`.

## Maps

A Map stores key-value pairs. The keys must be comparable (`==` operator).

An empty `map` (`string` keys and `int` values) is created using the `make`
builtin function:

    m := make(map[string]int)

Entries can be added/changed by assignment:

    m["age"] = 31

Values can be accessed by its key:

    age := map["age"] 

Trying to access non-existent entries returns the zero value of the value type:

    weight := map["weight"] // weight == 0

Maps can created using a literal:

    m := map[string]int{"a": 1, "b": 2, "c": 3}

## `if` Statement

TODO

### Combined `if` Statement

The `if` statement can be combined with a declaration and initialization, thus
removing the scope of the variable to the `if` block:

    if err := request.ParseForm(); err != nil {
        log.Fatal(err)
    }

## `continue` Statement

Jump to the next iteration of a loop:

    for i := 1; i < 10; i++ {
        if i % 2 == 0 {
            continue
        }
        fmt.Println(i)
    }

## `break` Statement

Leave the loop:

    i := 0
    for {
        if i == 10 {
            break
        }
        i++
    }

## Casting

Cast a byte slice to a string:

    s := string([]byte{65, 66, 67})
    fmt.Println(s) // ABC


## Constants

The `const` keyword defined a constant:

    const maxIndex = 255

Multiple constants can be combined to one declaration:

    const (
        firstIndex = 0
        lastIndex  = 255
    )

Constant declarations can appear at the package or function level.

## The `append` function

Add to a slice:

    s := []int{0, 1, 2}
    s = append(s, 2) // s == []int{0, 1, 2, 3}

## Composite Literals

### Slice

    fib := []int{1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89}

### Map

    pop := map[string]int{"Switzerland": 8, "Germany": 8, "Russia": 150}

### Struct

    type country struct {
        name       string
        population int
    }
    switzerland := country{name: "Switzerland", population: 8}

## Channels

Channels are created using the `make` builtin function, combined with the
`chan` keyword and with an according data type:

    ch := make(chan string)

Data is written to the channel using the arrow operator:

    ch <- "through the channel you go"

Data is read to che channel using the arrow operator, too:

    var str string
    str <- ch

## Go Routines

Any function call can be executed concurrently by preceding it with the `go`
keyword:

    foobar(foo, bar) // synchronous call
    go foobar(foo, bar) // asynchronuous call

## Mutex

A variable can be protected by a preceding mutex declaration:

    var mu sync.Mutex
    var count int

Any protected access to the variable must be surrounded by lock/unlock
instructions:

    mu.Lock()
    count++
    mu.Unlock()

## Switch

For multi-way branches, the `switch` statement is an option:

    switch resp.StatusCode {
        case 200:
            fmt.Println("OK")
        case 400:
            fmt.Println("client error")
        case 500:
            fmt.Println("server error")
        default:
            fmt.Println("something strange")
    }

There's no `break` needed to terminate the execution after a branch. The
`fallthrough` statement can be used to fall through to the next branch (a
tagless `switch` doesn't need an operand, it evaluates boolean expressions for
every case):

    switch {
        case i > 100:
            fmt.Println("bigger than hundred")
            fallthrough
        case i > 10:
            fmt.Println("bigger than ten")
            fallthrough
        case i > 1:
            fmt.Println("bigger than one")
    }

The `switch` statement can be combined with an initialization, limiting the
scope of the initialized variable to the `switch` block:

    switch i := rand.Intn(100); i {
        case 13:
            fmt.Println("what a coincidence")
        default:
            fmt.Println("whatever...")
    }


## Comments

Single-line comments start with `//` and span to the rest of the line:

    i++ // increment i

Multi-line comments start with `/*` and end with `*/`:

    /*
     * I wanted to delete this code.
     * But I was afraid.
     * i--
     */

## Pointers

Pointers are declared with an asterisk:

    var i int // normal variable
    var *p int // pointer variable

Pointers store the address of a variable, which can be obtained using the
ampersand (address-of operator):

    p = &i

The value can be assigned and used with the asterisk:

    fmt.Println(*p)
    *p = 3

## Type Declarations

New types can be defined based on existing types:

    type Celsius float32

This helps when methods should apply only for a custom type, not for the underlying general type:

    func (c Celsius) String() string {
        return fmt.Sprintf("%g°C", c)
    }

## Type Conversion

Every type `T` offers a conversion function `T()`:

    i := 100     // int
    j := int8(i) // int8
