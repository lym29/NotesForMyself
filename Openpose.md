## Environment
Since I need to use the openpose on a HPC sever, I started to learn how to use singularity container
```
pip install spython
```

### Prepare Container 
- Option 1: build on server
  Pull from the dockhub
  ```
  singularity pull cwaffles_openpose.sif dock://cwaffles/openpose:latest
  ```

- Option 2: build on local
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
