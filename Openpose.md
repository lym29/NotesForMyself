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
singularity build --fakeroot openpose.sif openpose.def
```
## Prepare Container (build on local)
>在本地将Dockerfile build成镜像并打包成.tar格式或将已有镜像直接导出成.tar格式，上传到集群后用Singularity将docker镜像转换成singulairty镜像，此步骤不需要管理员权限。
Need to create a new docker builder
https://prinsss.github.io/build-x86-docker-images-on-an-m1-macs/

```
docker buildx build --platform linux/arm,linux/arm64,linux/amd64 -t yumengliu/openpose . --push
```

