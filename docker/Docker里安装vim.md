# Docker里安装vim

在`Docker`里运行程序，有时候需要修改一些文件，可是当你

```shelll
vim [filenme]
```

的时候，往往会提示：

```shell
vim: command not found
```

当你

```shell
apt-get install vim
```

又出现

```shell
Reading package lists... Done  
Building dependency tree         
Reading state information... Done  
E: Unable to locate package vim
```

这时你需要

```shell
apt-get update
```

完成之后再次

```shell
apt-get  install vim
```

即可安装`vim`编辑器。