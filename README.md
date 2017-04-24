# Compilation

Note: QEMU must be compiled in 32-bit mode, otherwise the generated TCG will assume the host architecture is 64-bit!

On a 32-bit machine:
```
./configure --enable-debug --target-list=arm-softmmu,arm-linux-user
make
```

On a 64-bit Debian/Ubuntu machine with multiarch support for i386 (not recommended, requires various dependencies, e.g. `libpcre16-3:i386`, `libpcre3-dev:i386`, `libpcre32-3:i386`, `libpcrecpp0v5:i386`, `libglib2.0-dev:i386`, `zlib1g-dev:i386`, `libgcrypt20-dev:i386` `libgpg-eror-dev:i386`):
```
PKG_CONFIG_LIBDIR=/usr/lib/i386-linux-gnu/pkgconfig ./configure --enable-debug --enable-tcg-interpreter --target-list=arm-softmmu,arm-linux-user --extra-cflags="-m32" --extra-ldflags="-m32"
```

# Execution
```
./arm-linux-user/qemu-arm -d page,op_opt,out_asm,in_asm,cpu -L /usr/arm-linux-gnueabi ../verifIR/proofs/ocaml-code/test_program/add
ls -alh arm.bin tci.bin
```
