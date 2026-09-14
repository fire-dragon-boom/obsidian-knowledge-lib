## 常用命令
1. 查看wsl.exe 版本
	```powershell
	wsl -v
	```
2. 查看可安装的 Linux 发行版
	```powershell
	wsl --list --online
	#or 简写
	wsl -l -o
	```
3. 安装指定发行版本
	```powershell
	wsl --install -d Debian
	
	# 安装到指定位置
	wsl --install -d Debian --location D:\WSL\Debian
	```
4. 卸载指定发行版本
	```powershell
	wsl --unregister <发行版名称>
	```
5. 查看安装状况
	```
	wsl -l -v
	```
6. 启动wsl
	```powershell
	wsl -d Debian
	```
7. 停止wsl
	```powershell
	wsl -t Debian
	```
8. 停止所有wsl
	```powershell
	wsl --shutdown
	```
9. 以root用户进入
	```powershell
	wsl -d Debian -u root
	```
10. 退出系统
	```powershell
	exit
	```
11. 设置默认发行版
	```powershell
	wsl --set-default Debian
	```
12. 迁移发行版
	```powershell
	# 导出
	wsl --export Debian D:\debian.tar
	# 注销原发行版
	wsl --unregister Debian
	# 导入
	wsl --import Debian "F:\Program Data\WSL\Debian" D:\debian.tar --version 2
	# last 删除导出
	```
13. 设置默认启动用户
	进入配置文件
	```bash
	sudo nano /etc/wsl.conf
	```
	添加默认用户修改
	```ini
	[user]  
	default=admin
	```

# 网络
wsl使用虚拟网卡，单独的子网


# 无窗口启动-挂起进程
``` bash
powershell.exe -WindowStyle Hidden -c "wsl -d Debian sleep infinity"
```
- **原理**：该命令在后台以隐藏窗口模式启动了 Debian，并在内部执行了 `sleep infinity`（无限期休眠）。由于这个进程永远不会自动结束，WSL 就会一直保持 `Running` 状态。
- **如何关闭**：当你不需要它驻留后台时，在 Windows 终端执行 `wsl --shutdown` 即可彻底关闭。


# 开机启动

- 在 Windows 中按下 `Win + R`，输入 `shell:startup` 回车，这将打开 Windows 的**开机启动文件夹**。
- 在该文件夹下新建一个文本文件，重命名为 `wsl-background.vbs`（后缀必须是 `.vbs`）。
- 鼠标右键编辑该文件，写入以下内容
	```vbs
	Dim WshShell
	Set WshShell = CreateObject("WScript.Shell")
	WshShell.Run "powershell.exe -WindowStyle Hidden -c ""wsl -d Debian sleep infinity""", 0, False
	```


# 设置端口独立
修改用户目录下的.wslconfig文件

```ini
[wsl2]
localhostForwarding=false
```











