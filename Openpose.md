# Environment
Since I need to use the openpose on a HPC sever, I started to learn how to use singularity container
```
pip install spython
```

## Prepare Container （build on server)

fork the dockerfile from [https://github.com/myoshimi/openpose-docker](https://github.com/myoshimi/openpose-docker.git)

```
git clone https://github.com/lym29/openpose-docker.git
cd openpose-docker/
```
change the cuda version in the dockerfile

```
# convert the dockerfile to the *.def file
spython recipe Dockerfile &> openpose.def
singularity build --remote openpose.sif openpose.def
```
## Prepare Container (build on local)
Need to create a new docker builder
https://prinsss.github.io/build-x86-docker-images-on-an-m1-macs/

