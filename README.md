# Setup

Note: QEMU must be compiled in 32-bit mode, otherwise the generated TCG will assume the word length of the host architecture (64-bit on x86-64)!

On a 32-bit machine:
```
./configure --enable-debug --enable-tcg-interpreter --target-list=arm-softmmu,arm-linux-user
make
```

On a 64-bit Debian/Ubuntu machine with multiarch support for i386 (not recommended, certain packages are not multiarch enabled, will cause package conflicts, requires dependencies: `libpcre16-3:i386 libpcre3-dev:i386 libpcre32-3:i386 libpcrecpp0v5:i386 libglib2.0-dev:i386 zlib1g-dev:i386 libgcrypt20-dev:i386 libgpg-error-dev:i386`):
```
PKG_CONFIG_LIBDIR=/usr/lib/i386-linux-gnu/pkgconfig ./configure --enable-debug --enable-tcg-interpreter --target-list=arm-softmmu,arm-linux-user --extra-cflags="-m32" --extra-ldflags="-m32"
```

# Usage

Install the runtime libraries and dynamic loader:
```
sudo apt-get install libc6-armel-cross binutils-arm-linux-gnueabi
```

Execute an application under QEMU user-mode emulation, generating the necessary dumps:
```
ulimit -s 1024
./arm-linux-user/qemu-arm -d page,op_opt,out_asm,in_asm,cpu -L /usr/arm-linux-gnueabi ../verifIR/tcg-example/add
ls -alh arm.bin tci.bin image.bin
```
