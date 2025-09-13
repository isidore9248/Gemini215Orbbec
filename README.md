
### 访问Gemini Orbbec

1. 进入SDK/shared
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
2. 进入OrbbecViewer，运行OrbbecViewer，查看能否正常打开摄像头

### 编译c++程序

1. 进入SDK/example
```
mkdir build && cd build
cmake ..
make
```
2. 进入bin目录运行实例程序