# docker-xmrig-amd

Docker container for [xmrig-amd](https://github.com/xmrig/xmrig-amd) with AMD RX Vegas on Linux, including [AMDGPU-Unified Linux drivers](https://support.amd.com/en-us/kb-articles/Pages/Radeon-Software-for-Linux-Release-Notes.aspx), and donate level patch.

## Requirements

 * [docker](https://docs.docker.com/install/)

### The matching drivers on your host (choose one)

 * [AMDGPU-Unified Linux drivers 18.10](https://support.amd.com/en-us/kb-articles/Pages/Radeon-Software-for-Linux-Release-Notes.aspx)
 * [AMDGPU-Pro 17.50](https://www2.ati.com/drivers/linux/ubuntu/amdgpu-pro-17.50-552542.tar.xz)
 * [AMDGPU-Pro Beta Mining Driver 17.40](https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-Pro-Beta-Mining-Driver-for-Linux-Release-Notes.aspx)

On you host, install the drivers with a command similar to (read the Dockerfile for the version of drivers you want to use):

#### Examples

```
./amdgpu-pro-18.10-572953/amdgpu-pro-install -y --opencl=pal
```

OR

```
./amdgpu-pro-17.50-552542/amdgpu-pro-install -y --opencl=rcom
```

## Usage

### First

Pull the latest build:

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
docker build . --file 18.10/Dockerfile --tag bananajamma/xmrig-amd-vega:18.10
docker build . --file 17.50/Dockerfile --tag bananajamma/xmrig-amd-vega:17.50
docker build . --file 17.40-blockchain/Dockerfile --tag bananajamma/xmrig-amd-vega:17.40-blockchain
```

## FAQ

#### Does this work with more than one Vega?

I don't know, I only have one Vega right now.  I think it requires PCIe x16, and a [ROCm capable CPU](https://github.com/RadeonOpenCompute/ROCm#supported-cpus).  Let me know.

## License

MIT
