# docker-xmrig-amd-vega

Docker containers for [xmrig-amd](https://github.com/xmrig/xmrig-amd) with AMD RX Vegas on Linux, including various driver support, and donate level patch.

## Tags

 * `latest`, `18.10`
 * `17.50`
 * `17.40-blockchain`

## Requirements

 * [docker](https://docs.docker.com/install/)

### The matching drivers on your host (choose one)

 * [AMDGPU-Unified Linux drivers 18.10](https://support.amd.com/en-us/kb-articles/Pages/Radeon-Software-for-Linux-Release-Notes.aspx)
 * [AMDGPU-Pro 17.50](https://www2.ati.com/drivers/linux/ubuntu/amdgpu-pro-17.50-552542.tar.xz)
 * [AMDGPU-Pro Beta Mining Driver 17.40](https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-Pro-Beta-Mining-Driver-for-Linux-Release-Notes.aspx)

On you host, install the drivers with a command similar to (read the Dockerfile for the version of drivers you want to use):

#### Host Driver Installation

Below are examples of flags used when installing drivers on your host system to work with these docker containers.

##### 18.10

```
./amdgpu-pro-18.10-572953/amdgpu-pro-install -y --opencl=pal
```

##### 17.50

```
./amdgpu-pro-17.50-552542/amdgpu-pro-install -y --opencl=rcom
```

##### 17.40-blockchain

```
./amdgpu-pro-17.40-483984/amdgpu-pro-install -y
sudo apt install -y rocm-amdgpu-pro
```

## Usage

### First

Pull the latest build with the driver tag that you've installed on your host (example):

```
docker pull bananajamma/xmrig-amd-vega:18.10
```

### Running

Example:

```
docker run --device /dev/dri --device /dev/kfd --group-add=video -it --rm --name xmrig-amd-vega bananajamma/xmrig-amd-vega:18.10 --donate-level 0 -o gulf.moneroocean.stream:10032 -u 4JLN35ooAiU15BX6Rzi6DTWUKsdLALvf6Stx1uLLrYP28scYTAtyjhM3ULkrpCQMQ1BGvn2hSaYGtSzwtPcZhFSwdoFypnBsb6wKfhTGix -p x -k
```

### Building

If you've clone this repo and made changes:

```
docker build . --file 18.10.Dockerfile --tag bananajamma/xmrig-amd-vega:18.10 --tag bananajamma/xmrig-amd-vega:latest
docker build . --file 17.50.Dockerfile --tag bananajamma/xmrig-amd-vega:17.50
docker build . --file 17.40-blockchain.Dockerfile --tag bananajamma/xmrig-amd-vega:17.40-blockchain
```

## FAQ

#### Does this work with more than one Vega?

I don't know, I only have one Vega right now.  I think it requires PCIe x16, and a [ROCm capable CPU](https://github.com/RadeonOpenCompute/ROCm#supported-cpus).  Let me know.

## License

MIT
