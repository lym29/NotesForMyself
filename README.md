# NotesForMyself
**Table of contents**  

[Environment](./Environment.md)  

[Blender](./blender.md)

[others](./others.md)

**Useful Link**

[A blog introducing python API for load tf from bag files](https://zhuanlan.zhihu.com/p/449107970)

[Containerize a conda environment in a Singularity container](https://stackoverflow.com/questions/54678805/containerize-a-conda-environment-in-a-singularity-container)

**Network** 

If connection to github fails, add the below config to "~/.ssh/config" file:
```
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```
Remember to use SSH connection when trying to push/pull from github repo. 
```
git remote -v
```
Check the link of remote branch!
