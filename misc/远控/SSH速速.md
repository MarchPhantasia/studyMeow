``` shell
sudo apt-get update 						# 更新源
sudo apt-get upgrade						# 更新已安装包
sudo apt install openssh-server			# 安装ssh服务器
sudo apt install openssh-client			# 安装ssh客户机
sudo systemctl enable ssh
sudo systemctl start ssh
sudo ufw enable

sudo ufw allow ssh
sudo ufw allow 22
```

``` shell
# root 权限
# User privilege specification  
root ALL=(ALL) ALL  
username ALL=(ALL) ALL
```

``` shell
# sudo权限
sudo adduser username
sudo usermod -G sudo username
```
