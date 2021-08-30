# software

The toolchain for compiling programs will probably be later provided in a toolchain folder here, but for now you have to download it by yourself and change a few paths.

For more info about downloading the toolchain can be found here:
https://xpack.github.io/riscv-none-embed-gcc/install/

After you downloaded the toolchain, you probably will have to change a few paths in your program (currently the only program is cpu-programs/example-1). A more central path directory would be nice to have in the future. 

What you need to change:

In "MAKEFILE":
line 29: TOOLCHAIN_PATH = /opt/xpack-riscv-none-embed-gcc-10.1.0-1.1

In "BIN.py":
line 15: PATH_READELF='/opt/xpack-riscv-none-embed-gcc-10.1.0-1.1/bin/riscv-none-embed-readelf'
line 16: PATH_OBJDUMP='/opt/xpack-riscv-none-embed-gcc-10.1.0-1.1/bin/riscv-none-embed-objdump'

In "CREATE_LOGISIM_ROM.py":
line 6: PATH_LOGISIM_ROM = "/Users/filipszkandera/PINEAPPLE_program_logisim"

In "DUMP.py"
line 41: default='/opt/xpack-riscv-none-embed-gcc-10.1.0-1.1/bin/riscv-none-embed-objdump',


To test everything you can open a terminal in the same directory as your program and enter "make". If no errors are shows and it generated your logisim file (PATH_LOGISIM_ROM), you can put it into logisim for a test (more in cpu-simulation). A dissasembled version can be found in build/app.lss and you can compare it to "EXAMPLE_DISSASEMBLY.lss" if you haven't made any changes.


WARNING:
I had to change the linker script to some generic one, as the one I was using may have been propriatory. This linker is very basic bare-bones one and maybe does not provide all the capabilities.
Also this CPU cannot read a program memory by the program itself, so anything that would normally go into .bss, etc will be unused at the moment. This is the reason why I declare the variable first and then assign it a value. I hope I find a fix soon.