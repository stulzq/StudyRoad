# Linux

## 一.Linux常用命令

- 毁天灭地：`rm -rf /*` 新手绝对不可使用
### 1.1用户操作
- 创建用户：`useradd <username>`

- 给新创建的用户设置密码:`passwd <username>`

- 删除用户：`userdel <username>`

- 删除用户目录：`rm -rf <username>`

- 添加用户组：`groupadd <groupname>`

- 将用户添加到用户组：`usermod -G <groupname> <username>`

- 删除用户组：`groupdel <groupname>`

- 新建用户同时加入用户组：`useradd -g <groupname> <username> `

- [Linux新建用户如何添加root权限](Linux新建用户如何添加root权限.md)

  ​
