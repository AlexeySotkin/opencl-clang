Common clang is a thin wrapper library around clang. Common clang has OpenCL-oriented API and is capable to compile OpenCL C kernels to SPIR-V modules.

## Build

Source code in this repo is intended to be built in-tree as an llvm project. Before the build all dependencies must be downloaded and layed out as the following:

```
<workspace>
`-- llvm
    |-- tools
    |   `-- clang
    `-- projects
        |-- SPIRV-LLVM-Translator
        `-- common-clang
```
This can be done using the following commands:
```
cd <workspace>
git clone https://github.com/llvm-mirror/llvm.git -b release_70
cd tools
git clone https://github.com/llvm-mirror/clang.git -b release_70
cd <workspace>/llvm/projects
git clone https://github.com/KhronosGroup/SPIRV-LLVM-Translator.git
git clone https://github.com/intel/opencl-clang.git
```

Then run cmake and pass it llvm directory as an argument
After that common_clang target should be available in the build system.

