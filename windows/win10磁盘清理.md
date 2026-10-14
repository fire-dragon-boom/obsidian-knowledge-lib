# 占大头的可清理文件
## 1. onedrive
C:\Program Files\Microsoft OneDrive
这些数字文件夹是更新迭代产物
![](assets/win10磁盘清理/file-20261014171907939.png)

查看可执行文件，确认产品版本和修改日期，按时间倒序，删掉其他的数字文件夹
![](assets/win10磁盘清理/file-20261014172020602.png)

## 2. NVIDIA
C:\ProgramData\NVIDIA Corporation\Downloader
这个下面有一个残留的安装程序文件夹

C:\Users\Admin\AppData\Local\NVIDIA\DXCache
这是dx缓存，可以删除，再使用中就跳过

## 3. C:\ProgramData\Microsoft
![](assets/win10磁盘清理/file-20261014172841534.png)
### 3.1 search是索引结果，不要删除，通过重建来瘦身
![850](assets/win10磁盘清理/file-20261014173408933.png)

### 3.2 ClickToRun\ProductReleases
office应用旧版本安装文件缓存，可删除

### 3.3 Window Defender

1. **`Windows Defender\Definition Updates\Backup` (443 MB)**
    
    - **说明**：这是 Windows Defender 病毒库更新前的**旧版本备份**。
        
    - **操作**：**可以安全删除**。Defender 如果更新出问题，会自动重新下载，不需要这个旧备份。
        
2. **`Windows Defender\Definition Updates\{E707...}` (224 MB)**
    
    - **说明**：这通常是病毒库的某个临时更新包或残留。
        
    - **操作**：可以删除。通常 Defender 只保留最新的一个版本，旧版本可以清掉。



## 4. local/Temp临时文件夹
C:\Users\Admin\AppData\Local\Temp
这个文件夹下的东西直接删除


## 5. C:\Windows

#### 5.1 System32\DriverStore\FileRepository
windows 驱动备份仓库
使用DriverStoreExplorer软件来进行删除
![](assets/win10磁盘清理/file-20261014175913648.png)


#### 5.2 C:\Windows\assembly

![](assets/win10磁盘清理/file-20261014180225644.png)

- **说明**：这个文件夹存放的是 .NET Framework 的程序集（Assembly）。图里可以看到，最大的两个子文件夹是 `NativeImages_v4.0.30319_64` (1.9GB) 和 `NativeImages_v4.0.30319_32` (337MB)。
    
- 这是 Windows 为了加速 .NET 程序启动而生成的**本机映像缓存（Native Images）**。当 .NET 更新或安装新软件时，旧版本的缓存不会自动删除，就会堆积在这里。
    
- **如何安全清理（绝对不能直接删文件夹）**：
    
    1. 以**管理员身份**运行命令提示符（CMD）或 PowerShell。(经实践，需要使用**cmd管理员**)
        
    2. 输入以下命令并回车：  
        `%windir%\Microsoft.NET\Framework64\v4.0.30319\ngen.exe update`  
        （如果是32位系统，把 Framework64 改成 Framework）
        
    3. 这个命令会重新生成最新的缓存，并自动清理掉不再需要的旧版本文件。这个过程可能需要几分钟，请耐心等待。


## 6. C:\Users\Admin\AppData\Local

### 6.1 Google
C:\Users\Admin\AppData\Local\Google
![](assets/win10磁盘清理/file-20261014181118666.png)

chrome 不处理，删除旧版本的Android

