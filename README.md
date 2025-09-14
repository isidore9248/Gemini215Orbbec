
### Linux 访问Gemini Orbbec

1. 下载必要依赖
```
sudo apt update
sudo apt install libudev-dev libusb-dev
sudo apt install freeglut3
```

2. 安装miniconda
``` 
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-py39_4.9.2-Linux-aarch64.sh

bash Miniconda3-py39_4.9.2-Linux-aarch64.sh
```

3.  进入SDK/shared
```
sudo ./install_udev_rules.sh
```
!!! 重启或者插拔设备

- 备用
```
# 1. 复制规则文件（需要 root 权限）
sudo cp shared/99-obsensor-libusb.rules /etc/udev/rules.d/

# 2. 重新加载规则
sudo udevadm control --reload-rules

# 3. 重启 udev 服务
sudo udevadm trigger

# 4. 将当前用户添加到 video 用户组（可能需要重新登录生效）
sudo usermod -a -G video $USER
```


3. 查看设备
```
lsusb
cd /dev
ls
```
查看是否有 gemini


4. 试运行</br>
进入OrbbecViewer，运行OrbbecViewer，查看能否正常打开摄像头

### 编译c++程序

1. 进入SDK/example
```
mkdir build && cd build
cmake ..
make
```
2. 进入bin目录运行实例程序

### 编译python程序

1. 创建python3.9虚拟环境
2. 进入pyorbbecsdk 
3. 编译
```
mkdir build && cd build
mkdir build && cd build
cmake .. -DPYTHON_EXECUTABLE=$(which python)  # 指定Python路径
make -j4
make install
```
4. 添加环境变量

-  创建脚本文件
```
mkdir -p /home/isidore/miniconda3/envs/orbbec/etc/conda/activate.d /home/isidore/miniconda3/envs/orbbec/etc/conda/deactivate.d && chmod +x /home/isidore/miniconda3/envs/orbbec/etc/conda/activate.d/orbbec_env.sh /home/isidore/miniconda3/envs/orbbec/etc/conda/deactivate.d/orbbec_env.sh
```

- 在activate.d/orbbec_env.sh中添加
```
#!/bin/bash

# 添加SDK路径到PYTHONPATH
export PYTHONPATH=/home/isidore/Orbbec/pyorbbecsdk-2-main/install/lib:$PYTHONPATH

# 添加库路径到LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/isidore/Orbbec/pyorbbecsdk-2-main/install/lib:$LD_LIBRARY_PATH
```