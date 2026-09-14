## Introduction

**`exeluac` provides a ready-to-use command-line tool for packaging Lua scripts and Lua compiled files into standalone Windows executables.**

- `exeluac` is available in both 32-bit and 64-bit versions.
- **The 32-bit version of `exeluac` only includes 32-bit Lua interpreters and can only generate 32-bit executables.**
- **The 64-bit version of `exeluac` includes both 32-bit and 64-bit Lua interpreters, allowing you to generate either 32-bit or 64-bit executables.**
- The source code of `exeluac` itself is written in Lua and packaged as an exe.
- The conversion process is powered by [srlua](https://github.com/LuaDist/srlua).
- **This tool statically links with different Lua versions, so the generated exe does not require any external DLLs.**
- **Platform limitation: Windows 32/64-bit only.**

---

## Installation

1. Download the appropriate version of `exeluac` for your system architecture (32-bit or 64-bit) from the [releases page](https://github.com/NotAMark2/exeluac/releases).
2. Extract it to any directory, and add the extracted `exeluac` folder to your system `PATH` environment variable. Restart your terminal (or open a new one).
3. Run `exeluac -v` in a terminal. If it displays the version number, the installation was successful.

> Note: The `srlua` folder must be in the same directory as the program.

---

## Directory Structure

```
exeluac.exe
srlua\
	\5.1.5-32\
		srlua.exe
		srglue.exe
	\5.1.5-64\
		srlua.exe
		srglue.exe
	\5.4.6-32\
		srlua.exe
		srglue.exe
	\5.4.6-64\
		srlua.exe
		srglue.exe
	<...>
```

> The Lua interpreter version is customizable, as long as it follows the `<Lua version>-<Arch>` naming convention.
> 
> **The 32-bit version of exeluac only contains folders for 32-bit Lua versions (e.g., 5.1.5-32, 5.4.6-32, etc.), while the 64-bit version contains folders for both 32-bit and 64-bit Lua versions, allowing you to choose the corresponding architecture for the generated executable.**
>
> Make sure the selected Lua version matches the architecture of your `exeluac.exe`. A 32-bit `exeluac.exe` cannot use a 64-bit Lua interpreter, and vice versa.

---

## Usage

### Show Version

```batch
exeluac -v
```

### Show Help

```batch
exeluac -h
```

### List Available Lua Versions

```batch
exeluac --list
```

Sample output:

```
exeluac: available lua versions:

	- 5.1.5-32
	- 5.1.5-64
	- 5.4.6-32
	- 5.4.6-64

```

*(The 32-bit version of exeluac will only list 32-bit Lua versions, such as 5.1.5-32, 5.4.6-32, etc.)*

### Compile Lua Script to EXE

```batch
exeluac -c hello.lua hello.exe --lua 5.1.5-32
```

- `--lua <version>` specifies the interpreter version (must match the subfolder name under `srlua/`). If no matching version is available, a corresponding error message will be displayed.

---

## Command-Line Options

Both Unix-style (`-<short>` / `--<long>`) and DOS-style (`/<short or long>`) flags are accepted.

| Option | Description |
| --- | --- |
| `-v`, `--version`, `/v`, `/version` | Show exeluac version |
| `-h`, `--help`, `/h`, `/help` | Show help information |
| `--list`, `/list` | List all available Lua versions in the `srlua` folder |
| `-c`, `--compilate`, `/c`, `/compilate` | Compile the specified Lua file to exe |
| `--lua` `<version>`, `/lua` `<version>` | Specify Lua version (used with `-c`, `--compilate`, `/c`, `/compilate`) |

---

## Notes

- **exeluac only supports Windows 32/64-bit systems.**
- Each subfolder under `srlua\` must contain both `srlua.exe` and `srglue.exe` for that version.
- Not supported on Linux or macOS.
- The supported Lua versions are determined by the actual folders present under `srlua\`.
- **The 32-bit exeluac can only generate 32-bit exes; the 64-bit exeluac can generate either 32-bit or 64-bit exes depending on the selected Lua version.**
