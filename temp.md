


```js
	# 导出
	wsl --export Debian D:\debian.tar
	
	wsl --export Ubuntu D:\ubuntu.tar
	# 注销原发行版
	wsl --unregister Debian
	wsl --unregister Ubuntu
	# 导入
	wsl --import Debian "F:\Program Data\WSL\Debian" D:\debian.tar --version 2
	wsl --import Debian "F:\Program Data\WSL\Debian" D:\debian.tar --version 2
	# last 删除导出
```