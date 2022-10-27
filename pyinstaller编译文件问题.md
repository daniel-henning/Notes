### BUG ONE:

bug信息
```
[128115] WARNING: file already exists but should not: /tmp/_MEIBMiq3M/pyarrow/lib.cpython-36m-x86_64-linux-gnu.so
```

此bug在编译和运行过程中没有产生影响，消除该警告信息的具体操作如下：
首先找到.spec配置文件修改配置文件，在配置文件中加入以下代码：

```bash
for d in a.datas:
	if 'lib.cpython-36m-x86_64-linux-gnu.so' in d[0]:
		a.datas.remove(d)
		break
```

修改完文件后使用.spec重新编译程序即可解决该报错问题
```
pyinstaller -F *.spec
```
