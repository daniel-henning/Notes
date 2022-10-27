BUG ONE:

```
[128115] WARNING: file already exists but should not: /tmp/_MEIBMiq3M/pyarrow/lib.cpython-36m-x86_64-linux-gnu.so
```

上述bug在编译和运行过程中没有产生影响，但是自己在偶然的原因不知不觉的就解决了此bug，具体操作如下：
首先找到.spec配置文件修改配置文件，在配置文件中加入以下代码：

```bash
for d in a.datas:
	if '_C.cp37-win_amd64.pyd' in d[0]:
		a.datas.remove(d)
		break
```
