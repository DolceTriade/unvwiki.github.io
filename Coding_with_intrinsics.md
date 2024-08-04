---
title: Coding with intrinsics
permalink: /Coding_with_intrinsics/
---

For performance purpose, it is possible to implement alternative code
path using architecture-dependent code or compiler-dependent code.

It is important that code making use of such intrinsics code comes with
an alternative generic implementation as a fallback for portability and
debugging.

Usage of intrinsics can lead to great performance improvements,
especially in the engine code which is built natively for the user's
platform. Some engine code being shared with the game code as a
framework, such code may either use the optimized code (use case of a
game server using a native exe as server game code) or the generic
implementation. In the future when the port to WebAssembly is done even
the virtualized game code may start to make use of some Wasm intrinsics.

Common implementation examples are the usage of i686 SSE intrinsics for
vector operations.

There can be two kinds of intrinsics: Architecture-dependent intrinsics,
and Compiler-dependent intrinsics.

## Architecture-dependent intrinsics

Architecture-dependent intrinsics are provided by specific hardware
features like SSE on i686 or amd64, like NEON on arm64, or pure assembly
code.

Here is an example taken from the fast approximate inverse square root
code for i686 SSE:

`_mm_store_ss( &y, _mm_rsqrt_ss( _mm_load_ss( &number ) ) );`

Here is an example of fast approximate inverse square root for the
32-bit PowerPC platform, this code is not part of the Dæmon engine as
this platform is not supported but it is given as a good example of what
can be doable:

`asm( "frsqrte %0, %1" : "=f"( y ) : "f"( number ) );`

## Compiler-dependent intrinsics

Compiler-dependent intrinsics are provided by specific compiler
features.

Here is an example of implementation of the function for GCC and Clang:

`ans = __builtin_ctz( x );`

And here is the same for MSVC:

`_BitScanForward( &ans, x );`

## Generic alternative code

It is important that optimized code using intrinsics functions come with
alternative generic code as a fallback, this is useful both for
portability (make the port to a new platform or compiler easier) and
testing (one may compare the output of the various implementations).

When writing code, one can use the C/C++ definition to guard the code
making use of compiler intrinsics, and some of the definitions to guard
the code making use of architecture intrinsics.

Here are some examples of preprocessor definitions usable to guard
architecture intrinsics code:

-

-

The definition is automatically defined by the CMake code itself.

When a platform is a child of another platform, definitions for both are
defined, for example on amd64 both and are defined.

Extension-dependent definitions like are meant to be defined in using
architecture-specific definitions like when the definition is set.

When an extension is first defined in a parent platform, the definition
is defined for the parent platform, for example on amd64 the is defined,
and this definition is meant to be used for both i686 with SSE code path
and amd64 code path when architecture intrinsics are enabled.

It is asked to always use instead of within C/C++ preprocessor code to
make sure disabling the intrinsics code really disables it. The same
will be true if we implement similar definitions like in the future, it
would have to be preferred over .

## Toggling optimized and alternative code

We provide two CMake options and to make easy to enable or disable the
use of compiler or architecture optimized code. Those options are
enabled by default.