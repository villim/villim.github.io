---
title: Setup Golang Enviroment on Mac
layout: post
---

## 1. Install gcc compiler

### 1.1 Download

After register Apple Developer Account, you will be able to download **Command Line Tools ( macOS xx.xx ) for Xcode x.x**
from [Downloads for Apple Developers](https://developer.apple.com/download/more/)

### 1.2 Install

After install, you would see similar information:

```bash
➜  ~ gcc -v
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr --with-gxx-include-dir=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.13.sdk/usr/include/c++/4.2.1
Apple LLVM version 9.0.0 (clang-900.0.39.2)
Target: x86_64-apple-darwin17.4.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

## 2. Installing Golang 

### 2.1 Download

Download latest version from [Golang.org](https://golang.org/dl/). Currect version is **go1.9.4.darwin-amd64.pkg**

### 2.2 Install

I choose install for all users, and Go will be installed under **/usr/local/go**

```bash
➜  ~ ll -l /usr/local/go
total 264
-rw-r--r--    1 root  wheel    40K Feb  8 01:09 AUTHORS
-rw-r--r--    1 root  wheel   1.5K Feb  8 01:09 CONTRIBUTING.md
-rw-r--r--    1 root  wheel    54K Feb  8 01:09 CONTRIBUTORS
-rw-r--r--    1 root  wheel   1.4K Feb  8 01:09 LICENSE
-rw-r--r--    1 root  wheel   1.3K Feb  8 01:09 PATENTS
-rw-r--r--    1 root  wheel   1.6K Feb  8 01:09 README.md
-rw-r--r--    1 root  wheel     7B Feb  8 01:46 VERSION
drwxr-xr-x   15 root  wheel   480B Feb  8 01:53 api
drwxr-xr-x    5 root  wheel   160B Feb  8 01:53 bin
drwxr-xr-x    4 root  wheel   128B Feb  8 01:53 blog
drwxr-xr-x   46 root  wheel   1.4K Feb  8 01:53 doc
-rw-r--r--    1 root  wheel   5.6K Feb  8 01:09 favicon.ico
drwxr-xr-x    3 root  wheel    96B Feb  8 01:53 lib
drwxr-xr-x   16 root  wheel   512B Feb  8 01:53 misc
drwxr-xr-x    6 root  wheel   192B Feb  8 01:53 pkg
-rw-r--r--    1 root  wheel    26B Feb  8 01:09 robots.txt
drwxr-xr-x   68 root  wheel   2.1K Feb  8 01:53 src
drwxr-xr-x  286 root  wheel   8.9K Feb  8 01:53 test
```

### 2.3 Link to **/usr/bin** for convenient:

```bash
➜  ~ sudo ln -s /usr/local/go/bin/go /usr/bin/go
➜  ~ sudo ln -s /usr/local/go/bin/godoc /usr/bin/godoc
➜  ~ sudo ln -s /usr/local/go/bin/gofmt /usr/bin/gofmt
```

### 2.4 Verify 

Check what Golang can do with :

```bash
➜  ~ go help
```

For example, print Go environment information:

```bash
➜  ~ go env
GOARCH="amd64"
GOBIN=""
GOEXE=""
GOHOSTARCH="amd64"
GOHOSTOS="darwin"
GOOS="darwin"
GOPATH="/Users/williamwang/go"
GORACE=""
GOROOT="/usr/local/go"
GOTOOLDIR="/usr/local/go/pkg/tool/darwin_amd64"
GCCGO="gccgo"
CC="clang"
GOGCCFLAGS="-fPIC -m64 -pthread -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fdebug-prefix-map=/var/folders/bc/7jpj3vk11hn6kmh9spc_db3h0000gp/T/go-build870332584=/tmp/go-build -gno-record-gcc-switches -fno-common"
CXX="clang++"
CGO_ENABLED="1"
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
```

