# hola

<img src="https://img.shields.io/badge/Version-1.0.0-blue?style=flat-square" alt="Version">  
<img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License MIT">

**hola** is the simplest possible terminal greeting utility.

It prints:

```
¡Hola!
```

That's it.  
One command. One joyful line. Zero configuration. Perfect for welcoming yourself (or annoying your coworkers) every time you open a new terminal.

## Why does this exist?

- To say hello in Spanish with proper exclamation marks and inverted one
- To serve as a minimal educational example of a modern curl | sh style installer
- To have the shortest possible useful shell script with version checking, help, and self-installation logic
- Because sometimes you just want to type `hola` and feel a tiny bit happier

## Features

- Prints colorful `¡Hola!` in green
- Self-installs to `/usr/local/bin/hola` when run via `curl | sh`
- Asks for confirmation in interactive terminals
- Automatically installs in non-interactive environments (CI, piped curl)
- Contains `version` and `help` subcommands
- Very small codebase (~60 effective lines)

## Installation

The recommended (and fastest) way:

```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/hola/main/hola | sh
```

### What this command does:

1. Downloads the latest `hola` script
2. If already installed → does nothing
3. If **interactive terminal** → asks whether you want to install
4. If **non-interactive** (piped curl) → installs automatically
5. Copies itself to `/usr/local/bin/hola`
6. Makes it executable
7. Shows success message

**Need root privileges?** (common on Linux/macOS when writing to `/usr/local/bin`)

```bash
sudo curl -fsSL https://raw.githubusercontent.com/Wilgat/hola/main/hola | sudo sh
```

## Usage

```bash
hola
# → ¡Hola!   (in green)

hola version
# → hola version 1.0.0

hola help
# shows this help message
```

## Examples

```bash
# Most common uses
hola
hola && echo "Starting work now..."

# In scripts
#!/usr/bin/env bash
hola
echo "Welcome back!"
```

## Program Structure (for curious people)

The script is intentionally kept very simple:

```text
┌───────────────────────────────┐
│  Version & install path       │
├───────────────────────────────┤
│  Color definitions            │
├───────────────────────────────┤
│  is_installed() check         │
├───────────────────────────────┤
│  show_install_suggestion()    │ ← heart of the curl|sh magic
│    ├─ interactive prompt      │
│    └─ auto-install in pipe    │
├───────────────────────────────┤
│  Help text (heredoc)          │
├───────────────────────────────┤
│  Argument parsing             │
├───────────────────────────────┤
│  Install suggestion call      │
└───────────────────────────────┘
          ↓
     Main command switch
     (display / version / help)
```

## Contributing

This project is deliberately minimal.  
The most useful contributions would be:

- Making the greeting multilingual / randomized
- Adding funny variants (`hola --sassy`, `hola --pirate`, etc.)
- Better platform detection / install locations
- GitHub Actions to publish releases

## License

[MIT License](LICENSE)

Made with ♥ and one line of joy  
2025–2026
