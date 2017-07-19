## linux服务器配置

### SSH
一种网络协议,用于计算机之间的加密登录，采用公匙加密，远程主机发送公匙给用户，用户用公匙加密后发送回远程主机，然后
远程主机再用私匙解密．初次登录远程主机会提示保存远程主机公匙，一般是～/.ssh/known_hosts,下次登录跳过提示警告
```
$ ssh　user@host
$ ssh -p 222 user@host //默认端口是22,修改
```
建立自己的公匙，存入远程主机上后就可以公匙登录
```
$ ssh-keygen  //在~/.ssh/目录下会生成两个文件 id_rsa.pub,id_rsa
```



远程登录:
```
$ ssh root@xx.xx.xx.xx //远程登录
$ passwd //修改密码
$ addgroup admin //创建用户组
$ useradd -d /home/miao -s /bin/bash -m bill //创建用户,指定用户主目录,和shell,如果不存在则创建目录
$ passwd mhq  //设置密码
$ usermod -a -G admin miao //将用户miao加入到用户组admin
$ visudo    //设定sudo权限,打开/etc/sudoers
//加入 miao ALL=(ALL)NOPASSWD:ALL, 切换sudo的时候不需要密码
//本机SSH设置，用ssh-keygen生成一个SSH公匙
$ cat ~/.ssh/id_ras.pub | ssh miao@xx.xx.xx.xx 'mkdir -p .ssh && cat ->> ~/.ssh/authorized_keys' //本机操作,将本机公匙拷贝到服务器的authorized_keys文件,或者下面的操作
$ ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
//在服务器上编辑SSH配置文件 /etc/ssh/sshd_config
$ vi /etc/ssh/sshd_config //可以先备份，后编辑修改一些配置文件
$ service ssh  restart //重启SSHD
```




参考：

[http://www.ruanyifeng.com/blog/2014/03/server_setup.html](http://www.ruanyifeng.com/blog/2014/03/server_setup.html)

[http://spenserj.com/blog/2013/07/15/securing-a-linux-server/](http://spenserj.com/blog/2013/07/15/securing-a-linux-server/)


