---
title: "Hello Go Jetson Nano"
date: 2023-05-18T10:51:03+05:30
draft: false
---


## We are going to run an Golang binary in Jetson nano.

First write a simple go program.

```
package main

import "fmt"

func main() {
	fmt.Println("Hello Jetson Nano!")
}

```

Compile for arm64 on linux. If your platform is different, use below list to figure it out.

```
go tool dist list | grep arm           
android/arm
android/arm64
darwin/arm64
freebsd/arm
freebsd/arm64
ios/arm64
linux/arm
linux/arm64
netbsd/arm
netbsd/arm64
openbsd/arm
openbsd/arm64
plan9/arm
windows/arm
windows/arm64
```

In Jetsons case it linux/arm64

So to compile for Nano (you will have to create arm64bins directory).

`env GOOS=linux GOARCH=arm64 go build -o ./arm64bins/jetson`

You will get a binary for linux/arm64. Scp it to the host box and run.

```
:~$ ./jetson 
Hello Jetson Nano!
```

Let go overboard and do a make file. Crate a **makefile** with following content.

```
BINARY_NAME=jetson

build:
	env GOOS=linux GOARCH=arm64 go build -o ./arm64bins/${BINARY_NAME}

clean:
	go clean
	rm -rf ${BINARY_NAME}
```

Very straightforward!!