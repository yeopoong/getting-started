Go
===

Install
-------

```
$ wget https://storage.googleapis.com/golang/go1.6.2.linux-amd64.tar.gz  
$ sudo tar -C /usr/local -xzf go1.6.2.linux-amd64.tar.gz  
```

환경설정
-------

`.bash_profile`
```
export PATH=/usr/local/go/bin:$PATH
```

```
$ go env 
$ go version 
```

GOROOT 설정
```
export GOROOT=$HOME/go 
```

Tip: 설치 경로가 /usr/local/go 또는 C:\Go 라면 GOROOT를 설정할 필요가 없다.

GOPATH 설정
```
export GOPATH=$HOME/go/work 
```

```
$ sudo go get golang.org/x/tools/cmd/...
```

Hello
-----

```go
package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}
```

Reference
---------

[Getting Started](https://golang.org/doc/install?download=go1.10.3.windows-amd64.zip)
[디스커버리 Go](https://github.com/jaeyeom/gogo)
