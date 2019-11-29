# Geode-go
Go version go1.13.4 linux/386 built with appropriate flags to support AMD Geode processors (lack of SSE instruction vs typical i386 go compilation)

Prerequisites: gcc and git

1. Install Go 1.4 bootstrap compiler sources in C with all the fixes from [Install Go compiler binaries](https://dl.google.com/go/go1.4-bootstrap-20171003.tar.gz) section of [Installing Go from source](https://golang.org/doc/install/source) guide

```
from your work directory
> wget https://dl.google.com/go/go1.4-bootstrap-20171003.tar.gz
> tar -xzf go1.4-bootstrap-20171003.tar.gz
> cd go
> cd src
```

2. Export variables
```
export GOROOT_BOOTSTRAP=$HOME/<your-work-dir>/go
export GO386=387
export GOARCH=386
export GOOS=linux
export CGO_ENABLED=0 
```

**Note the GO386=387 flag**

3.
```
GOOS=linux GOARCH=386 GO386=387 ./make.bash
```

4. Check supported architecture (should be GOARCH=386)
```
> cd..
> cd bin
> cd linux_386
> ./go env
GOARCH="386"
GOBIN=""
GOCHAR="8"
GOEXE=""
GOHOSTARCH="386"
GOHOSTOS="linux"
GOOS="linux"
GOPATH=""
GORACE=""
GOROOT="/home/<user>/<work-dir>/go"
GOTOOLDIR="/home/<user>/<work-dir>/go/pkg/tool/linux_386"
CC="gcc"
GOGCCFLAGS="-fPIC -m32 -fmessage-length=0"
CXX="g++"
CGO_ENABLED="0"
```

5. Go to the directory you want your latest go compiler version to go to <new-work-dir> and download sources
```
> mkdir src
> cd src
> git clone https://go.googlesource.com/go goroot
> cd goroot
> git checkout go1.13.4
> cd src  
```
  
5. Compile
```
GOOS=linux GOARCH=386 GO386=387 CGO_ENABLED="0" ./make.bash
Installed Go for linux/386 in /home/<user>/<new-work-dir>/src/goroot
Installed commands in /home/<user>/<new-work-dir>/src/goroot/bin
```

Note that the resulting binary will be in /home/<user>/<new-work-dir>/src/goroot/bin/linux_386. Change to that directory and run ```./go env``` to confirm. Output should be similar to
  
```
GO111MODULE=""
GOARCH="386"
GOBIN=""
GOCACHE="/home/<user>/.cache/go-build"
GOENV="/home/<user>/.config/go/env"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="386"
GOHOSTOS="linux"
GONOPROXY=""
GONOSUMDB=""
GOOS="linux"
GOPATH="/home/rhy-ama/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/home/<user>/<new-work-dir>/src/goroot"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/home/<user>/<new-work-dir>/src/goroot/pkg/tool/linux_386"
GCCGO="gccgo"
GO386="387"
AR="ar"
CC="gcc"
CXX="g++"
CGO_ENABLED="0"
GOMOD=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m32 -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build761101590=/tmp/go-build -gno-record-gcc-switches"

```

Note that the Go (golang) is distributed under [this](https://github.com/golang/go/blob/master/LICENSE) license subject to the following copyright notice: ```Copyright (c) 2009 The Go Authors. All rights reserved.```

**Sources:**

[Installing Go from source](https://golang.org/doc/install/source)

[How to Write Go Code](https://golang.org/doc/code.html)
