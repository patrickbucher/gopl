# Conventions

## `main` Package

A package with the name `main` declares a standalone program (as
compared to a library).

## `main()` Function

The function `main()` in the `main` package is the starting point of a
standalone program.

## `init()` Function

The function `init()` in every package is called upon the package's
initialization, before `main` that is.

    var i = 1
    var f = 1.1
    var s = "foo"

    func init() {
        i = 2
        f = 2.2
        s = "bar"
    }

    func main() {
        fmt.Println(i, f, s) // prints 2 2.2 bar
    }

## Braces

Opening Braces must not stand on a new line.

## Package Comments

A package is described by a comment of one or more sentences immediately
preceding the `package` declaration:

    // Package strings implements simple functions to manipulte UTF-8 encoded
    // strings.
    package strings

If the package consists of multiple file, only one file should contain the
package comment. This usually is the file with the name of the package itself
(`foobar` package: `foobar.go`). To keep the source file short and clean,
documentation can also be put into a file called `doc.go`.

The comment preceding the `main` package describes the program as a whole:

    // Echo prints its command-line arguments.
    package main

## Verbs for Formatted Output

The functions in the `fmt` package with a `f` at the end of their names support
formatted output using _verbs_:

- integers
    - `%d`: decimal integer, `10`
    - `%x`/`%X`: hexa-decimal integer, `af9832`/`AF9832`
    - `%o`: octal integer, `245243`
    - `%b`: binary integer, `10011010110`
- floating point numbers
    - `%f`: single precision float, `3.333333`
    - `%g`: double precision float, `3.3333333333333335`
    - `%e`: exponential representation, `3.333333e+00` (`3.333333 * 10^0`)
- boolean
    - `%t`: boolean, `true` or `false`
- text
    - `%c`: rune (unicode code point), `ç`
    - `%s`: string, `élément`
    - `%q`: quoted string (`"c'est quoi, ça?"`) or quoted rune (`'ç'`)
- miscellaneous
    - `%v`: value of an expression in natural format
        - `fmt.Println("%v", fmt.Println) // 0x47c070`
        - `fmt.Println("%v", 10/3.0) // 3.3333333333333335`
    - `%T`: type of an expression
        - `fmt.Println("%v", fmt.Println) // func(...interface {}) (int, error)`
        - `fmt.Println("%v", 10/3.0) // float64`
    - `%%`: literal `%`

### Adverbs

If an argument is needed twice:

    fmt.Printf("%v %T\n", 10/3, 10/3)

It can be reused using the `[1]` adverb:

    fmt.Printf("%v %[1]T\n", 10/3)

The adverb can deal with any positive number >0 within the arguments index
range.

The prefix of octal and hexadecimal numbers can be printed using the `#` adverb:

    fmt.Printf("%#o %#x %#X\n", 10, 10, 10)
    // 012 0xa 0XA

The two adverbs mentioned can be combined:

    fmt.Printf("%#o %#[1]x %#[1]X\n", 10)
    // 012 0xa 0XA

Integers can be right aligned using the width adverb:

    fmt.Printf("%6d\n", 1)
    fmt.Printf("%6d\n", 1000)
    fmt.Printf("%6d\n", 1000000)

Output:

          1
       1000
    1000000

Floating point number can be aligned using the width adverb. The first number
indicates  the overall width of the number to print, including the decimal
positions. The second number indicates the positions after the decimal point:

    fmt.Printf("%6.2f\n", 10/3.0)
    fmt.Printf("%6.2f\n", 10/3.0)
    fmt.Printf("%6.2f\n", 10/3.0)

Output:

        3.33
       33.33
      333.33

## Escape Sequences

- `\n`: new line
- `\t`: tab
- `\\`: backspace

## Naming

### Exported Names

Names starting with a capital letter are exported, others not:

type Person struct {
    Firstname   string  // exported
    Lastname    string  // exported
    identity    int     // not exported
}

### Camel Case

Go identifiers are written in CamelCase:

    var yearOfBirth, durationInMillis int   // good
    var year_of_birth, duration_in_milis    // bad

Acronyms should be spelled in all capitals:

    var exportedToHTML bool // good
    var exportedToHtml bool // bad

## Import Path

The import path `org.acme/encabulator` is looked up in the directory
`$GOPATH/src/org.acme/encabulator`
