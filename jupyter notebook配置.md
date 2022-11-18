## 1. 生成配置文件
`jupyter notebook --generate-config`


## 2. 设置密码
`jupyter notebook password`


## 3. 修改配置文件

`
vim ~/.jupyter/jupyter_notebook_config.py

#修改以下三个节点的配置，并把开头的 # 注释去掉
c.NotebookApp.ip = '*' # 开启所有的IP访问，即可使用远程访问
c.NotebookApp.open_browser = False # 关闭启动后的自动开启浏览器
c.NotebookApp.port = 8888  # 设置端口8888，也可用其他的，比如1080，8080等等

#修改工作目录
c.NotebookApp.notebook_dir = "工作路径"
`

## 4. 启动notebook
`jupyter notebook`


## 5. 主题
`pip install jupyterthemes`
`
# list available themes
# onedork | grade3 | oceans16 | chesterish | monokai | solarizedl | solarizedd
jt -l

# select theme...
jt -t chesterish
`

## 端口转发（mobaxterm 的ssh tunneling 可快速实现）
windows端实现服务器端口转发。
`
netsh interface portproxy add v4tov4 listenaddress=10.6.16.112 listenport=8080 connectaddress=compute-1-1 connectport=7789 

#删除一个端口转发。

netsh interface portproxy delete v4tov4 listenaddress=10.6.16.112 listenport=8080

ssh -i /amoydx/USER/hening/config/mycert.pem -N -L localhost:7789:10.6.16.112:7789 hening@10.6.16.112

ssh -i /amoydx/USER/hening/config/mycert.pem -N -L localhost:7789:10.6.16.112:7789 hening@10.6.16.12

netstat -ntlp   //查看当前所有tcp端口·
netstat -ntulp |grep 80   //查看所有80端口使用情况·
netstat -ntulp | grep 7789   //查看所有7789端口使用情况·

ssh -i /amoydx/USER/hening/config/mycert.peN -L 172.17.42.177789:10.6.16.112:7789 hening@10.6.16.12222
`
