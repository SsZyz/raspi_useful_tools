参考: https://learn.microsoft.com/zh-cn/dotnet/core/install/linux-ubuntu-2204
0,环境依赖
sudo apt-get update && \
  sudo apt-get install -y libc6 libgcc1 libgcc-s1 libgssapi-krb5-2 libicu70 liblttng-ust1 libssl3 libstdc++6 libunwind8 zlib1g
注意:
(如果 .NET 应用使用 System.Drawing.Common 程序集，则还需要安装 libgdiplus。 由于 Linux 上不再支持 System.Drawing.Common，因此这仅适用于 .NET 6，并且需要设置 System.Drawing.EnableUnixSupport 运行时配置开关。)

1,官方提供的apt源安装方法

sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-x.x
sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-x.x
sudo apt-get update && \
  sudo apt-get install -y dotnet-runtime-x.x
其中根据内容的包含关系
  dotnet-sdk > aspnetcore-runtime > dotnet-runtime
但根据源的提供方,可能会出现版本延迟的问题.(例如2023-12-31日,无论是Ununtu源还是Microsoft源都还没提供linux系统arm64平台的dotnet_8.0的安装路径)

2,官方提供的脚本安装方法
wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
chmod +x ./dotnet-install.sh
./dotnet-install.sh --version latest
./dotnet-install.sh --version latest --runtime aspnetcore
./dotnet-install.sh --channel 8.0
该方法使用的网络储存在国内访问速率很低,大多数情况很能下载成功.

3,纯手动安装
从 https://dotnet.microsoft.com/zh-cn/download/dotnet/ 获取对应平台对应版本的下载地址
cd ~
wget https://download.visualstudio.microsoft.com/download/****/dotnet-sdk-*****-linux-arm64.tar.gz
sudo mkdir /usr/share/dotnet
sudo tar -zxvf dotnet-sdk-*****-linux-arm64.tar.gz -c /usr/share/dotnet
# install for user
vim .bashrc
DOTNET_ROOT=/usr/share/dotnet
PATH=$PATH:$DOTNET_ROOT
source .bashrc
# install for all user
sudo vim /etc/profile
DOTNET_ROOT=/usr/share/dotnet
PATH=$PATH:$DOTNET_ROOT
sudo reboot
