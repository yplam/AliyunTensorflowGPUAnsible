# AliyunTensorflowGPUAnsible

阿里云GPU服务器部署Tensorflow的Ansible脚本，主要用于快速初始化Tensorflow GPU环境，节省每次训练或测试的时间与成本

本脚本非通用脚本，只在UBUNTU 18.04、cuda 10.0.1、cudnn 7.4.2 tensorflow 1.13 上测试，请根据自己需求进行相应修改

欢迎交流：yplam#yplam.com (#=@)

cuda_repo: cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64
cudnn_repo: libcudnn7_7.4.2.24-1+cuda10.0_amd64
cudnn_dev_repo: libcudnn7-dev_7.4.2.24-1+cuda10.0_amd64

使用：

1、 注册nvidia开发者
2、 在 https://developer.nvidia.com/cuda-10.0-download-archive 下载 10.0.0 版本 CUDA Toolkit 到 roles/nvidia/files，修改 server.yml 对应配置项
3、 在 https://developer.nvidia.com/rdp/cudnn-archive 下载 7.4.2 版本 cuDNN Runtime Library for Ubuntu18.04 (Deb)， cuDNN Developer Library for Ubuntu18.04 (Deb) 到 roles/nvidia/files，修改 server.yml 对应配置项
4、（可选，推荐）如果你本地网络较慢，可以将下载的三个deb文件上传到阿里云 OSS，将其设置成公共读，然后修改 upload_cuda_cudnn_deb 为 false，并且配置 cuda_url, cudnn_url, cudnn_dev_url，这样可以节省大量时间，同样，你也可以将模型文件、dataset 等提前上传到阿里云 OSS，然后将地址配置到 data_files，脚本会下载到 /root/data 目录
5、 运行下面命令，下载依赖：

```
ansible-galaxy install --roles-path ./roles -r requirements.yml
```

6、阿里云购买 GPU 机器，如 ecs.gn5-c4g1.xlarge
7、登录 ECS，修改 vim ~/.ssh/authorized_keys ，将本地机器 key 加上去，用于免密登录(也可以创建是使用秘钥对登录，跳过此步)
8、修改 server 文件，将阿里云主机 ip 写进去
9、运行，完成（大概耗时二十分钟）

```
ansible-playbook -i server server.yml
```
