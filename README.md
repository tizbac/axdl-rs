# axdl-rs Unofficial Axera image downloader implementation in Rust

This is an unofficial Axera image downloader implementation in Rust to write image file into Axera SoCs.

[日本語](./README.ja.md)

## Table of Contents

- [Prepare](#Prepare)
- [Build](#build)
- [Usage](#usage)
- [License](#license)

## Prepare

### Linux 

In order to access to the device from a normal user, you have to configure udev to allow a normal user to access the device.
To configure udev, copy `99-axdl.rules` into `/etc/udev/rules.d` and reload the configuration of udev.

```
sudo cp 99-axdl.rules /etc/udev/rules.d/
sudo udevadm control --reload
```

## Build

Before building the project, install the Rust toolchain via rustup.

```bash
# Clone the repository
git clone https://github.com/ciniml/axdl-rs.git

# Change directory
cd axdl-rs

# Build
cargo build
```

## Usage

To burn a *.axp image, run the command below and plug the Axera SoC device with download mode.
For M5Stack Module LLM, keep press the BOOT button and plug the USB cable into the device.

```shell
cargo run --bin axdl-cli -- --file /path/to/image.axp --wait-for-device
```

If you don't want to burn the rootfs, specify `--exclude-rootfs` option.

```shell
cargo run --bin axdl-cli -- --file /path/to/image.axp --wait-for-device --exclude-rootfs
```

On Windows or other platforms where the official Axera AXDL driver is installed, you can use serial port access by specifying the --transport serial option:

```shell
cargo run --bin axdl-cli -- --file /path/to/image.axp --wait-for-device --transport serial
```

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.