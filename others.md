> environment.yml ResolvePackageNotFound
> https://github.com/datitran/object_detector_app/issues/41
> running this first conda config --set restore_free_channel true and then conda env create -f etc solved it for me
```
conda config --set restore_free_channel true
```
---  


**运行ros**  
https://zhuanlan.zhihu.com/p/85664330

---  


**服务器X11 forwarding相关设置**  
https://stackoverflow.com/questions/38961495/x11-forwarding-request-failed-on-channel-0  

---  

**Vscode 设置 X11**  
需要用private key登陆服务器  
服务器安装插件：[Remote X11](https://marketplace.visualstudio.com/items?itemName=spadin.remote-x11)  
本地安装插件：[Remote X11 (ssh)](https://marketplace.visualstudio.com/items?itemName=spadin.remote-x11-ssh)  
