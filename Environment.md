## Openpose
I am attempting to use the openpose on a HPC sever, so starting to learn how to use singularity container.  
spython can convert Dockerfile into singularity definition file
```
pip install spython
```

### Prepare Container 
- Option 1: **build on server**  
  Pull from the dockhub
  ```
  singularity pull cwaffles_openpose.sif docker://cwaffles/openpose:latest
  ```

- Option 2: **build on local**  
  >在本地将Dockerfile build成镜像并打包成.tar格式或将已有镜像直接导出成.tar格式，上传到集群后用Singularity将docker镜像转换成singulairty镜像，此步骤不需要管理员权限。
  
  Since my OS is arm architecture. I need to create a new docker builder, following the instruction below
  https://prinsss.github.io/build-x86-docker-images-on-an-m1-macs/
  
  ```
  docker buildx build --platform linux/arm,linux/arm64,linux/amd64,linux/x86 -t yumengliu/openpose . --push
  ```

### Run image
```
singularity exec cwaffles_openpose.sif /bin/bash
```
### Install openpose
```
[Singularity> cd openpose
[Singularity> mkdir build && cd build
[Singularity> cmake-gui ..
[Singularity> make -j32
```
**An annoying problem I met:** 
```
nvcc fatal   : Unsupported gpu architecture 'compute_80'
```
**Solution:** Find from this [issue](https://github.com/NVIDIA/cuda-samples/issues/44). Need to remove the "80 86" from the CUDA_ARCH_BIN args in the CMake config.
![image](https://github.com/lym29/NotesForMyself/assets/42018173/0d626447-ca88-4fef-8b31-7b526c5f2599)


## ROS
pull a ubuntu image from docker, run the container and install ros in it.  
[Installation](http://wiki.ros.org/noetic/Installation/Ubuntu)  

Got network issues when init the rosdep
find solution [here](https://www.debugpoint.com/failed-connect-raw-githubusercontent-com-port-443/)  
Following the first step, the problem is solved.

## Open3d
Dockerfile for Open3d
```
# This could also be another Ubuntu or Debian based distribution
FROM ubuntu:22.04

# Install Open3D system dependencies and pip
RUN apt-get update && apt-get install --no-install-recommends -y \
    libegl1 \
    libgl1 \
    libgomp1 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Install Open3D from the PyPI repositories
RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir --upgrade open3d
```
Use spython to convert it into singularity definition file.  
```
spython recipe Dockerfile open3d.def
singularity build --remote open3d.sif open3d.defsingularity build --remote open3d.sif open3d.def
```

## Unidexgrasp
> ".../miniconda/envs/unidexgrasp/lib/python3.8/site-packages/torch/utils/tensorboard/__init__.py", line 4, in <module>  
> LooseVersion = distutils.version.LooseVersion  
> AttributeError: module 'distutils' has no attribute 'version'
>
```
pip uninstall setuptools
pip install setuptools==59.5.0
```


## psbody-mesh
makefile issues when using python 3.8 to install psbody-mesh
```
no such option: --install-option
make: *** [Makefile:7: all] Error 
```
[Solution](https://github.com/MPI-IS/mesh/issues/89)


