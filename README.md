# ICCP-Setup

`explore-mms` is a command-line tool for inspecting devices that provide an MMS server (IEC 61850, EN 61850-8-1). The program connects to a specified MMS server and outputs information about the server identity, supported features, domains, and domain variables in JSON format.

## Installation & Deployment

The zeek script created by `explore-mms` is based on the MMS zeek plugin and the corresponding protocol stack. These zeek plugins can be installed using `zkg unbundle mms-1.0.bundle`. Alternatively, the plugins can be built and installed manually as described in [MMS](https://github.com/DINA-community/icsnpp-mms). 

Since the binary is **statically linked**, it can be used on almost any recent Linux system (x86-64) without requiring the `libiec61850` library to be installed on the system.

Just copy the generated `explore-mms` binary anywhere and execute it directly.

**Example:**
```sh
./explore-mms --help
```

## Usage and Parameters

The program can be started with the following parameters:

```
explore-mms [--password PASSWORD] [hostname [port]]
```

### Options:

`--help`:
: Displays the help screen.

`--password PASSWORD`:
: Uses ACSE password authentication during connection setup.

### Arguments:

`hostname`:
: Hostname or IP address of the MMS server. (Default: `localhost`)

`port`:
: MMS server's TCP port. (Default: `102`)

### Examples:

- Default call (no authentication, local): `explore-mms`
- With password authentication and explicit IP: `explore-mms --password secret 192.168.1.1`
- With all parameters: `explore-mms --password secret 192.168.1.1 102`

## Building and Compilation

**Requirements:**

- [CMake](https://cmake.org/)
- [libiec61850](https://libiec61850.com) (tested with version 1.5.1)
- A C Compiler (e.g., gcc)

**Build steps:**

```sh
mkdir build
cd build
cmake ..
make
```

The resulting binary `explore-mms` will be located in the build folder.

## Dependencies

To build and run, you need:

- **libiec61850** (tested with version **1.5.1**), including its headers and static library (`libiec61850.a`)
- Standard C library

`explore-mms` is linked **statically** against `libiec61850` and other system libraries where possible. There are no runtime dependencies.


## Notes

- All program results (except error messages) are written as JSON to `stdout`.
- Errors and exceptions are output in human-readable form to `stderr` and cause program termination.
- The exit code is non-zero on any error.

## License

The software was developed on behalf of the BSI (Federal Office for Information Security)

Copyright (c) 2025 by DINA-Community BSD 3-Clause. [See License](/COPYING)
