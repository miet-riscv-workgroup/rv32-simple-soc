rv32-simple-soc
===============

```
$ sudo apt-get install git
$ git clone --recursive https://github.com/miet-riscv-workgroup/rv32-simple-soc
$ cd rv32-simple-soc
```


toolchain
---------

```
$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev \
        libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc \
        zlib1g-dev

$ cd riscv-gnu-toolchain
$ sudo mkdir /opt/riscv
$ sudo chown $USER /opt/riscv
$ ./configure --prefix=/opt/riscv --with-arch=rv32i
$ make linux
```


QEMU
----

```
$ sudo apt-get install python pkg-config zlib1g-dev libglib2.0-dev

$ cd riscv-qemu
$ ./configure --target-list=riscv32-softmmu,riscv64-softmmu --prefix=/opt/riscv
$ make install
```


nmon
----

```
$ cd riscv-nmon
$ make nmon_picorv32-wb-soc_10MHz_9600.bin CROSS_COMPILE=/opt/riscv/bin/riscv32-unknown-linux-gnu-


$ /opt/riscv/bin/qemu-system-riscv32 -nographic -M erizo \
         -bios nmon_picorv32-wb-soc_10MHz_9600.bin \
         -serial stdio -monitor none -trace file=/dev/null
```


fusesoc
-------

```
$ sudo apt-get install python-pip
$ cd fusesoc
$ sudo pip install -e .
```

### fusesoc: simulation

```
$ sudo apt-get install iverilog gtkwave
$ sudo apt-get install libelf-dev

$ cd riscv-soc-cores
$ fusesoc --cores-root cores/ sim marsohod2-picorv32-wb-soc
$ gtkwave build/marsohod2-picorv32-wb-soc_0/sim-icarus/picorv32-wb-soc.vcd
```


### fusesoc: build Altera Cyclone bitstream

```
$ cd riscv-soc-cores
$ export PATH=$PATH:/opt/altera/13.1/quartus/bin
$ fusesoc --cores-root cores/ build marsohod2-picorv32-wb-soc
```
