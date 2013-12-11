# My dotfiles

Various preferences for vim, zsh, etc. Symlinks dotfiles to their correct locations. Also contains files I use every day to automate things.
You can optionally symlink these to your /usr/bin directory to globally execute them.

## Usage

### Dotfiles
* Install with `rake install`
* Uninstall with `rake uninstall`

### Useful executables
* Install with 'rake binfiles'
* Todo: Uninstalling

## Binfiles

These are simple executable scripts that I use to automate small tasks.

### hlog

This parses the output of a `heroku logs` command for the given app, and shows you useful data on your dyno.
You must have runtime-metrics enabled. https://devcenter.heroku.com/articles/log-runtime-metrics.

Example: `hlog myapp`

## What is this?

See [this](http://dotfiles.github.io/) for more info.
