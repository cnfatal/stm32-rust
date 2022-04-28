# stm32-led

simple led light control write on rust,run on stm32f103c8t6.

for more rust embedded infomation check [the embedded Rust book][book].

[book]: https://rust-embedded.github.io/book

## Build&Flash

```sh
cargo build
cargo objcopy  --bin stm32-led --release --  -O binary boot.bin
sudo stm32flash -i '-dtr&rts,dtr&rts' -w boot.bin -v -g 0x0   /dev/cu.usbserial-10
```

## Debug

```sh
openocd -f interface/cmsis-dap.cfg -f target/stm32f1x.cfg -c 'transport select swd'
```

## Dependencies

### openocd

```sh
LIBUSB1_CFLAGS=$(pkg-config --cflags libusb) LIBUSB1_LIBS=$(pkg-config --libs libusb) CAPSTONE_CFLAGS=$(pkg-config --cflags capstone) CAPSTONE_LIBS=$(pkg-config --libs capstone) 
```

To build embedded programs using this template you'll need:

- latest rust toolchain

- `rust-std` components (pre-compiled `core` crate) for the ARM Cortex-M targets. Run:

```console
rustup target add thumbv6m-none-eabi thumbv7m-none-eabi thumbv7em-none-eabi thumbv7em-none-eabihf
```

## VS Code

This template includes launch configurations for debugging CortexM programs with Visual Studio Code located in the `.vscode/` directory.  
See [.vscode/README.md](./.vscode/README.md) for more information.  
If you're not using VS Code, you can safely delete the directory from the generated project.
