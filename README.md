# Waku

### **1. Setting Up a Validator Node for Waku (Nwaku)**

#### **Step 1: Install Prerequisites**

Before setting up the Waku node, ensure your system meets the following requirements:

- **Operating System:** Linux or macOS (experimental support for Windows)
- **Memory:** Minimum 2GB RAM (0.5GB for Relay nodes)
- **Disk Space:** 10GB+
- **Network:** Stable internet connection
- **Dependencies:**
  - C Compiler (e.g., GCC)
  - GNU Make
  - Bash
  - Git
  - Rust (installed via Rustup)
  - PostgreSQL Client Library (for certain features)

To install these dependencies, follow the appropriate commands based on your operating system:

- **Debian/Ubuntu:**

  ```bash
  sudo apt-get update
  sudo apt-get install build-essential git libpq5 jq
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  source "$HOME/.cargo/env"
  ```

- **Fedora:**

  ```bash
  sudo dnf install @development-tools git libpq-devel
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

- **macOS:**

  Install Homebrew if not already installed:

  ```bash
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```

  Then, install the required packages:

  ```bash
  brew install cmake git postgresql@15 rustup-init
  sudo mkdir -p /usr/local/lib/
  sudo ln -s /opt/homebrew/opt/postgresql@15/lib/libpq.5.dylib /usr/local/lib/libpq.dylib
  ```

#### **Step 2: Clone the Waku Repository**

Clone the Waku (Nwaku) repository to your local machine. This repository contains the source code and all necessary components to build and run a Waku node.

```bash
git clone https://github.com/waku-org/nwaku
cd nwaku
```

You are now in the `nwaku` directory where you will perform the build and configuration steps.

#### **Step 3: Build the Waku Node**

Build the `wakunode2` binary, which is the core component of the Waku node:

```bash
make wakunode2
```

The first time you run `make`, it will automatically update all Git submodules. If you update your repository later, remember to run:

```bash
make update
```

This will ensure that all submodules are kept up-to-date.

#### **Step 4: Run the Waku Node**

After building, the `wakunode2` binary will be located in the `./build/` directory. Start your Waku node with:

```bash
./build/wakunode2
```

If you wish to see all available command-line options, you can run:

```bash
./build/wakunode2 --help
```

This command will display all possible configurations and modes in which you can run your node.

#### **Step 5: Configure Peer Discovery and Network Connection**

To effectively connect your Waku node to the network, you need to configure peer discovery. There are several methods to achieve this, such as:

- **DNS Discovery:** Use a DNS bootstrap node to discover peers.
- **Static Peers:** Manually configure known peers.
- **DiscV5:** An advanced peer discovery protocol.

Example to run with DNS discovery:

```bash
./build/wakunode2 --dns-discovery --dns-discovery-url=YOUR_DNS_BOOTSTRAP_NODE_URL
```
