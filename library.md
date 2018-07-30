# Library

## `fmt`

### `Println`

    func Println(a ...interface{}) (n int, err error)
        Println formats using the default formats for its operands and writes
        to standard output. Spaces are always added between operands and a
        newline is appended. It returns the number of bytes written and any
        write error encountered.

## `os`

### `Args`

    var Args []string
        Args hold the command-line arguments, starting with the program name.

## `strings`

### `Join`

    func Join(a []string, sep string) string
        Join concatenates the elements of a to create a single string. The
        separator string sep is placed between elements in the resulting
        string.

    func Split(s, sep string) []string
        Split slices s into all substrings separated by sep and returns a slice
        of the substrings between those separators.

        If s does not contain sep and sep is not empty, Split returns a slice
        of length 1 whose only element is s.

        If sep is empty, Split splits after each UTF-8 sequence. If both s and
        sep are empty, Split returns an empty slice.

        It is equivalent to SplitN with a count of -1.
