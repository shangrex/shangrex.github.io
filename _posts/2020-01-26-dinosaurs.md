---
layout: post
title: "Ubuntu install Cuda & Cundd"
subtitle: ""
date: 2020-01-26 23:45:13 -0400
background: '/img/night_ocean.jpeg'
---


# Ubuntu 裝cuda+cudnn
* 想要了解cuda, cudnn是甚麼的話可以參考一下網址
[reference](https://blog.csdn.net/u014380165/article/details/77340765)
* 主要操作官方[document](https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html)
* 以下範例都會是我的環境 ubuntu18.04+cuda11.0+x86_64
## 先裝nvidia驅動軟體
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install ubuntu-drivers-common
ubuntu-drivers devices
```
```
sudo apt install nvidia-driver-<version>
sudo reboot 
```
>ex. sudo apt install nvidia-driver-430


## 裝CUDA
基本上按照上面的指令
https://developer.nvidia.com/cuda-downloads?target_os=Linux

確認是哪一個Architecture，要不然之後會有error
```
uname -i
```
以我自己ubuntu18.04 x86_的指令
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/11.0.2/local_installers/cuda-repo-ubuntu1804-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1804-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```
這時候如果使用
```
nvidia-smi
```
可以看到cuda已經安裝好了
設置環境變數
```
export PATH=/usr/local/cuda-11.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
這樣就會可以使用指令
```
nvcc -V
```
## 裝CUDNN
* 依次下載，且依次安裝
![](https://i.imgur.com/hmze1iB.png)
![](https://i.imgur.com/oUD7CNH.png)

* 可參考官網code做測試