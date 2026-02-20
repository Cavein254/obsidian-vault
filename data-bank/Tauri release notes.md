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
FROM ubuntu:20.04

# Prevent prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    build-essential \
    libwebkit2gtk-4.0-dev \
    libssl-dev \
    libgtk-3-dev \
    libayatana-appindicator3-dev \
    librsvg2-dev \
    git \
    pkg-config

# Install Node.js (Version 20)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

WORKDIR /app

# Copy your project files
COPY . .

# Install frontend dependencies
RUN npm install

# Command to build (verifying that compilation works on 20.04)
CMD ["npm", "run", "tauri", "build"]
```

---

### 2. Build and Run the Container

Open your terminal in your project root and run these two commands:

### **Step A: Build the Image**

Bash

```bash
docker build -t tauri-test-20-04 -f Dockerfile.test .
```

### **Step B: Run the Build**

Bash

```bash
docker run --rm -v $(pwd)/src-tauri/target:/app/src-tauri/target tauri-test-20-04
```

> **Note:** The `-v` (volume) flag maps your local `target` folder to the container's. This way, once the build finishes inside Docker, the resulting `.AppImage` will appear in your local project folder.

---

## 3. Dealing with Graphical Errors (Testing vs. Building)

Docker containers are "headless" by default (no screen).

- **To check if it compiles:** The steps above work perfectly.
    
- **To actually run and see the UI:** This is much harder in Docker because you have to share your X11 or Wayland socket.
    

If you want to **launch** the app from inside Docker to see the window:

Bash

```
docker run -it --rm \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    tauri-test-20-04 npm run tauri dev
```

_(You may need to run `xhost +local:docker` on your host Ubuntu 24.04 first to allow the container to access your screen)._

---

## 4. Why 20.04?

When you compile code, it links against a library called **glibc**.

- **Ubuntu 24.04** uses a very new version.
    
- If you build there, your app **will not open** on older systems (like Debian 11 or Ubuntu 20.04) because their glibc is "too old."
    
- By building on **Ubuntu 20.04**, your app becomes "backwards compatible."
    

Would you like me to help you modify your **GitHub Action** to use this Docker container strategy so you never have to worry about Linux compatibility again?