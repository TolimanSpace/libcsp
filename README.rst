Toliman-related info
--------------------

This is a fork of the libcsp library, with some modifications to make it work with Toliman. The main changes are:
- Repository's main branch is on v1.6 (the latest published version of libcsp), with some modifications we added
- Added a nix environment (`shell.nix` and `.envrc`) to easily set up the environment for building. Make sure you have Nix and direnv installed to make use of this.
- Fixed a single debug warning that prevented compiling in -Werror mode
- Modified the Python bindings to be compatible with Python 3.10

Compiling:
```
# Configure
./waf configure --enable-python3-bindings --enable-shlib --prefix=$out --install-csp --enable-if-zmqhub --enable-can-socketcan --with-driver-usart=linux

# Build
./waf build
```

The Cubesat Space Protocol
==========================

Cubesat Space Protocol (CSP) is a small protocol stack written in C. CSP is designed to ease communication between distributed embedded systems in smaller networks, such as Cubesats. The design follows the TCP/IP model and includes a transport protocol, a routing protocol and several MAC-layer interfaces. The core of `libcsp` includes a router, a connection oriented socket API and message/connection pools.

The protocol is based on a 32-bit header containing both transport and network-layer information. Its implementation is designed for, but not limited to, embedded systems such as the 8-bit AVR microprocessor and the 32-bit ARM and AVR from Atmel. The implementation is written in GNU C and is currently ported to run on FreeRTOS, Linux (POSIX), MacOS and Windows. The primiary platforms being used are FreeRTOS and Linux.

The idea is to give sub-system developers of cubesats the same features of a TCP/IP stack, but without adding the huge overhead of the IP header. The small footprint and simple implementation allows a small 8-bit system to be fully connected on the network. This allows all subsystems to provide their services on the same network level, without any master node required. Using a service oriented architecture has several advantages compared to the traditional mater/slave topology used on many cubesats.

 * Standardised network protocol: All subsystems can communicate with eachother
 * Service loose coupling: Services maintain a relationship that minimizes dependencies between subsystems
 * Service abstraction: Beyond descriptions in the service contract, services hide logic from the outside world
 * Service reusability: Logic is divided into services with the intention of promoting reuse.
 * Service autonomy: Services have control over the logic they encapsulate.
 * Service Redundancy: Easily add redundant services to the bus
 * Reduces single point of failure: The complexity is moved from a single master node to several well defined services on the network

The implementation of `libcsp` is written with simplicity in mind, but it's compile time configuration allows it to have some rather advanced features as well:

Features
--------

 * Thread safe Socket API
 * Router task with Quality of Services
 * Connection-oriented operation (RFC 908 and 1151).
 * Connection-less operation (similar to UDP)
 * ICMP-like requests such as ping and buffer status.
 * Loopback interface
 * Very Small Footprint in regards to code and memory required
 * Zero-copy buffer and queue system
 * Modular network interface system
 * OS abstraction, currently ported to: FreeRTOS, Linux (POSIX), MacOS and Windows
 * Broadcast traffic
 * Promiscuous mode
 * Encrypted packets with XTEA in CTR mode
 * Truncated HMAC-SHA1 Authentication (RFC 2104)

LGPL Software license
---------------------
The source code is available under an LGPL 2.1 license. See COPYING
for the license text.

As a special exception, the copyright holders of libcsp gives you
permission to use macros or inline functions, or to link libcsp with
independent modules that communicate with libcsp solely through the
libcsp API interface, regardless of the license terms of these
independent modules, and to copy and distribute the resulting combined
work under terms of your choice.  However the source code for libcsp
must still be made available in accordance with the GNU Lesser General
Public License version 2.1.
