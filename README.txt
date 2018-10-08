Common clang is a thin wrapper library around clang. Common clang has OpenCL-oriented API and is capable to compile OpenCL C kernels to SPIR-V modules.

How to build

To build common clang inside llvm tree you need download it's dependencies and prepare the following layout:

 llvm
 |-- tools
 |   `-- clang
 |-- projects
     |-- SPIRV-LLVM-Translator
     `-- common-clang

 Then run cmake and pass it llvm directory as an argument
 After that common_clang target should be available in the build system.
 
