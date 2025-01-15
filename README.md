# ptunnel-ng-static

A statically linked version of [ptunnel-ng](https://github.com/utoni/ptunnel-ng), a tool for tunneling TCP connections over ICMP packets, making it portable and dependency-free.

## Features
- Static binary compilation for compatibility across Linux systems.
- Portable binary with no runtime dependencies.
- Step-by-step guide for building and installing.

## Prerequisites
Before you begin, ensure the following are installed on your system:

- `gcc` or another C compiler
- `make`
- `wget`
- Development tools and libraries:
  ```bash
  sudo apt update
  sudo apt install build-essential libssl-dev
  ```

## Compiled Binary

A precompiled statically linked binary is included in this repository for convenience. You can find it in the `bin` directory. To use it, simply download and execute:

```bash
chmod +x ./bin/ptunnel-ng
./bin/ptunnel-ng
```

## Build Instructions

### Step 1: Download and Build OpenSSL with Static Libraries

To ensure the static libraries for OpenSSL (`libcrypto.a`) are available, follow these steps:

```bash
wget https://www.openssl.org/source/openssl-3.3.2.tar.gz
tar -xvzf openssl-3.3.2.tar.gz
cd openssl-3.3.2
./config no-shared
make -j$(nproc)
sudo make install
```

### Step 2: Clone the ptunnel-ng Repository

Clone the official `ptunnel-ng` repository:

```bash
git clone https://github.com/utoni/ptunnel-ng.git
cd ptunnel-ng
```

### Step 3: Compile ptunnel-ng with Static Linking

Build the `ptunnel-ng` binary with static linking:

```bash
LDFLAGS="-static -L/usr/local/lib" CFLAGS="-I/usr/local/include" ./configure
make clean
make
```

### Step 4: Verify the Binary

Ensure that the binary is statically linked:

```bash
file ./ptunnel-ng
```
The output should include `statically linked`.

### Step 5: Install the Binary

For system-wide usage, install the binary to the `/opt` directory and create a symbolic link:

```bash
sudo mkdir -p /opt/ptunnel-ng
sudo mv ./ptunnel-ng /opt/ptunnel-ng/
sudo chmod 755 /opt/ptunnel-ng/ptunnel-ng
sudo ln -s /opt/ptunnel-ng/ptunnel-ng /usr/local/bin/ptunnel-ng
```

### Step 6: Test the Installation

Run the binary to verify that it works:

```bash
ptunnel-ng
```

## License
This project is licensed under the [MIT License](LICENSE).

## Acknowledgments
Special thanks to [utoni](https://github.com/utoni) for the original `ptunnel-ng` project.

## Contributing
Contributions are welcome! Please fork this repository and submit a pull request with your changes.
