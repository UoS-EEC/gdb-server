GDB server implementation in C++
===================================

This is a fork from the SystemC-linked [GDB server](https://www.embecosm.com/appnotes/ean7/html/ch01.html) from Embecosm.

It was modified to support more generic targets (e.g. MSP430, Cortex M0), using a C++ interface, and to remove the dependency on SystemC.

Installation:
===================================

Dependencies
-----------------------------------

Install [gabime/spdlog](https://github.com/gabime/spdlog), e.g. by running:

```bash
git clone https://github.com/gabime/spdlog.git
cd spdlog && mkdir build && cd build
cmake .. && make -j
sudo make install
```

Install
-----------------------------------

``` bash
git clone https://git.soton.ac.uk/sts1u16/gdb-server.git
cd gdb-server && mkdir build && cd build
cmake .. && make -j
sudo make install
```

Including in other CMake projects:
==================================

Add the following to your `CMakeLists.txt` file:

``` cmake
find_package(gdb-server REQUIRED)

# ...

target_link_libraries(myProject ... gdb-server::gdb-server)
```

Include the header in your source `.cpp` file:

``` c++
#include <gdb-server/GdbServer.hpp>
```

Example usage:
======

``` c++
#include <chrono>
#include <thread>
#include <gdb-server/GdbServer.hpp>
// ...
GdbServer gdbServer(/*Simulation controller =*/&simCrtl, /*tcp port=*/51000);
std::thread gdbThread(&GdbServer::serverThread, gdbServer);
// ...
```
