# AF_XDP L2 Forwarding

## Introduction

This is a simple L2 forwarding program using AF_XDP.

Daemon loads the kernel BPF program and pins the XSKMAP to the specified path. User client creates the XSK and starts listening on the specified interface. When the user client receives a packet, it processes the packet and transfers ownership of the packet to the kernel via the XSK umem.

## Project architecture

![Untitled-2023-11-18-2228_dark](https://github.com/xeome/af_xdp-l2fwd/assets/44901648/1fa453b2-414b-434c-afe8-5ce034ca71dd)


## Build

You need libxdp and libbpf installed.

```sh
make
```

## Usage

### Setup test environment

```sh
sudo ./testenv/testenv.sh setup --name=test
```

### Run

#### Daemon

```sh
sudo bin/xdp_daemon -d test --filename obj/xdp_kern_obj.o
```

#### User client

```sh
sudo bin/xdp_user -d test -p
```

#### Test

```sh
eval $(./testenv/testenv.sh alias)
t ping
```
