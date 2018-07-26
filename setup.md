# Setup

Install Go on Arch Linux:

    # pacman -S go

## Environment Variables

### GOROOT

Go's installation directory:

    export GOROOT='/usr/lib/go'

### GOPATH

The directory containing Go code:

    export GOPATH="$HOME/go"

Make sure to have the following folders in `$GOPATH`:

- `src`: source code
- `bin`: binaries
- `pkg`: packages

    mkdir -p $HOME/go/src
    mkdir -p $HOME/go/bin
    mkdir -p $HOME/go/pkg

### PATH

Add Go binaries to the PATH variable:

    export PATH="$PATH:$GOPATH/bin"
