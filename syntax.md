# Syntax

## Assignment

## `for` Loop

## Increment/Decrement

The increment and decrement operators are short forms of adding/subtracting one:

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

## String Concatenation

The `+` operator concatenates two strings:

    a := "foo"
    b := "bar"
    c := a + b // "foobar"

String concatenation can be combined with an assignment operator:

    a := "foo"
    a += "bar" # "foobar"

## Variable Declaration
