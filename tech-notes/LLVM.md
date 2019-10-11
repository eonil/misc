LLVM
====
Eonil, 2019


How to build?
-------------
Clone repo and just follow [official manual](https://lldb.llvm.org/resources/build.html#regular-in-tree-builds).

There are caveats.
- LLDB requires `libc++` stuff, but it seems macOS lacks it.
- Error is cryptic and hard to decode.

Here's my command that worked. 
Note that `-DLLDB_INCLUDE_TESTS=OFF` part to disable building test suite.

1. Clone repo.
2. Make and move to a new empty dir.
3. Run CMake there with passing LLVM source repo dir.

  cmake -G Xcode -DLLVM_ENABLE_PROJECTS="clang;lldb" -DLLDB_INCLUDE_TESTS=OFF ../llvm-project/llvm
  
This is for LLVM 9.0 including LLDB.

Maybe you need to install CMake using Homebrew.
