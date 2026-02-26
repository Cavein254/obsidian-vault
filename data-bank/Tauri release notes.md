## Initial Steps
Make the following changes to versions

```bash
"version": "0.2.0" // package.json, src-tauri/tauri.conf.json, src-tauri/Cargo.toml
```
1. create a tag
```bash
git tag -a v0.2.0 -m "Release version 0.2.0"
```
- `-a`: Creates an annotated tag (includes who tagged it, when, and a message).
- `-m`: The message describing this version.
2. Push the tag to github
```bash
git push origin v0.2.0
```

##  Testing Linux
### 1. Create a `Dockerfile`

Create a file named `Dockerfile.test` in your project root. This environment mimics the requirements we discussed earlier but specifically for the 20.04 LTS.

Dockerfile

```
# Use Ubuntu 22.04 for maximum AppImage compatibility (GLIBC)
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
# Required for AppImage tools to run inside Docker
ENV APPIMAGE_EXTRACT_AND_RUN=1 

# 1. Install System Dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    build-essential \
    pkg-config \
    libssl-dev \
    libgtk-3-dev \
    libwebkit2gtk-4.1-dev \
    libayatana-appindicator3-dev \
    librsvg2-dev \
    git \
    libfuse2 \
    file \
    && rm -rf /var/lib/apt/lists/*

# 2. Install Node.js 20 (LTS)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs

# 3. Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

# 4. Workspace setup
WORKDIR /app

# We don't COPY the code here because we will mount it at runtime 
# to get the build artifacts back out easily.
CMD ["npm", "run", "tauri", "build"]
```

---

### 2. Build and Run the Container

Open your terminal in your project root and run these two commands:

### **Step A: Build the Image**

Bash

```bash
docker build -t tauri-test-22-04 -f Dockerfile.test .
```

### **Step B: Run the Build**

Run this whenever you want to generate your AppImage:

Bash

```
docker run --rm -v "$(pwd):/app" tauri-test-22-04
```

**Breakdown of the command:**

- `--rm`: Automatically deletes the container after the build finishes (saves disk space).
    
- `-v "$(pwd):/app"`: **The Bind Mount.** It takes your current folder (`$(pwd)`) and maps it to `/app` inside the container.
    
- The `CMD` in the Dockerfile kicks in and starts the build.