# Conventions

## `main` Package

A package with the name `main` declares a standalone program (as
compared to a library).

## `main()` Function

The function `main()` in the `main` package is the starting point of a
standalone program.

## Braces

Opening Braces must not stand on a new line.

## Package Comments

A package is described by a comment of one or more sentences immediately
preceding the `package` declaration:

    // Package strings implements simple functions to manipulte UTF-8 encoded
    // strings.
    package strings

The comment preceding the `main` package describes the program as a whole:

    // Echo prints its command-line arguments.
    package main
