# Installation

The Tenderly CLI is a Go program, so we compile just a single binary that you can download and use. The basic installation process would be to download [the latest binary from the releases page](https://github.com/Tenderly/tenderly-cli/releases/latest) and move it somewhere in your `$PATH` so you can use it globally.

For everyone's convenience we have simplified the process explained above so you can install the Tenderly CLI just by running the following commands.

## Installing on macOS

Via [Homebrew](https://brew.sh/):

```
brew tap tenderly/tenderly
brew install tenderly
```

or via cURL (the command just downloads the latest release and moves it to `/usr/local/bin`):

```
curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-macos.sh | sh
```

## Installing on Linux
The command just downloads the latest release and moves it to `/usr/local/bin`:
```
curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh | sh
```

## Installing on Windows

Windows support coming soon!
