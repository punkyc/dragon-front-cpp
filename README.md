# A simple compiler front end

This is the complementation of c++ based on the source code of the complete compiler front end in the appendix of "Compilers: Principles, Techniques, and Tools, 2/e".

**Building the project after getting the source code** 

```
cmake -S ../dragon-front-cpp -B build
cd build 
make
```

**Requirements**

Before you build the project, ensure you have installed the LLVM project. And import $llvm_install_path  to `~/.bashrc` .

`export PATH=$llvm_install_path:$PATH`

**Translating testcases into LLVM IR**

```
./build/CompilerFrontCpp <tests/block1.t >tests/block1.ll
```

Then, we can use `llc` to convert `.ll` files to the assembly files(eg: `block1.s`). And use riscv-gnu-toolchain to link and obtain the elf files which can run in qemu. 

```
llc --march=riscv64 block1.ll
riscv32-unknown-elf-gcc block1.s -o block1
./qemu-project/build/qemu-riscv32 block1
```

