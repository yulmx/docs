
```Bash
useradd -r -m -s /bin/zsh <username>

password <username>
```
-r: 建立系统账号  
-m: 自动建立用户的登入目录  
-s：指定用户登入后所使用的shell

配置sudoer权限
```Bash
chmod +w /etc/sudoers # 该文件默认只读
vim /etc/sudoers
chmod -w /etc/sudoers # 恢复只读权限
```
vim添加内容
```Vim
# User privilege specification
root       ALL=(ALL:ALL) ALL
<username>   ALL=(ALL:ALL) ALL
```