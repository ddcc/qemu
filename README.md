# Compilation
```
./configure --enable-debug --enable-trace-backends=simple --target-list=arm-softmmu,arm-linux-user
make
```

# Execution
```
./arm-linux-user/qemu-arm -d page,op_opt,out_asm,in_asm,cpu -L /usr/arm-linux-gnueabi ../verifIR/proofs/ocaml-code/test_program/add
ls -alh arm.bin tci.bin
```
