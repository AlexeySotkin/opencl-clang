#
#  Copyright (c) 2018, Intel Corporation
# 
#  Permission is hereby granted, free of charge, to any person obtaining a
#  copy of this software and associated documentation files (the "Software"),
#  to deal in the Software without restriction, including without limitation
#  the rights to use, copy, modify, merge, publish, distribute, sublicense,
#  and/or sell copies of the Software, and to permit persons to whom the
#  Software is furnished to do so, subject to the following conditions:
# 
#  The above copyright notice and this permission notice shall be included
#  in all copies or substantial portions of the Software.
# 
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
#  OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
#  THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR
#  OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
#  ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
#  OTHER DEALINGS IN THE SOFTWARE.
#

#
# Common clang
#

project( ocl-fe )

cmake_minimum_required(VERSION 2.8)

find_package(Git REQUIRED)

set(LLVM_URL https://github.com/llvm-mirror/llvm.git)
set(LLVM_BRANCH release_60)

set(CLANG_URL https://github.com/AlexeySotkin/clang)
set(CLANG_BRANCH ocl-fe-60)

set(SPIRV-LLVM_URL https://github.com/KhronosGroup/SPIRV-LLVM-Translator)
set(SPIRV-LLVM_branch master)


function(git_clone repository branch directory)
    if (NOT EXISTS ${directory})
        message("Cloning from ${repository}")
        execute_process(COMMAND ${GIT_EXECUTABLE} clone --progress --branch ${branch} --single-branch ${repository} ${directory})
    endif()
endfunction()


git_clone(${LLVM_URL}       ${LLVM_BRANCH}       ${CMAKE_CURRENT_SOURCE_DIR}/llvm)
git_clone(${CLANG_URL}      ${CLANG_BRANCH}      ${CMAKE_CURRENT_SOURCE_DIR}/llvm/tools/clang)
git_clone(${SPIRV-LLVM_URL} ${SPIRV-LLVM_branch} ${CMAKE_CURRENT_SOURCE_DIR}/llvm/projects/SPIRV-LLVM-Translator)
file(COPY ${CMAKE_SOURCE_DIR}/cclang DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/llvm/projects)


if (EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/llvm")
    set(LLVM_TARGETS_TO_BUILD "X86" CACHE STRING "X86 only" FORCE)
    set(BUILD_SHARED_LIBS      TRUE CACHE BOOL   "Create shared libs" FORCE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/llvm)
endif()
