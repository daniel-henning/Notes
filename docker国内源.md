``` bash
vi /etc/docker/daemon.json

# 内容如下：
{
  "registry-mirrors": [
    "https://xx4bwyg2.mirror.aliyuncs.com",
    "http://f1361db2.m.daocloud.io",
    "https://registry.docker-cn.com",
    "http://hub-mirror.c.163.com",
    "https://docker.mirrors.ustc.edu.cn"
  ]
}{}

# 退出并保存
:wq

# 使配置生效
systemctl daemon-reload

# 重启Docker
systemctl restart docker
```
