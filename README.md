# AliyunTensorflowGPUAnsible

用于阿里云GPU服务器部署Tensorflow的Ansible脚本，主要用于快速初始化Tensorflow GPU环境，节省每次训练或测试的时间与成本

本脚本非通用脚本，只在UBUNTU 16.04、cuda 8、tensorflow 1.3 上测试，请根据自己需求进行相应修改

欢迎交流：yplam#yplam.com (#=@)

使用：

1、 注册nvidia开发者，将对应的 cuda deb文件与 cudnn tgz压缩包下载到 roles/nvidia/files，修改 server.yml 对应配置项

2、 运行下面命令，下载依赖：

```
ansible-galaxy install --roles-path ./roles -r requirements.yml
```

3、购买阿里云GPU服务器，将本地key加到服务器 ~/.ssh/authorized_keys 文件

4、运行，完成（大概耗时二十分钟）

```
ansible-playbook -i server server.yml
```
