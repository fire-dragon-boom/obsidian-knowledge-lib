# nodejs



## npm

### 1. 设置命令

```bash
npm config set cache "F:\ProgramData\nodejs_package_manager\npm\cache"
npm config set prefix "F:\ProgramData\nodejs_package_manager\npm\global"
```

执行后，可以用下面命令确认是否写入成功：

```bash
npm config get cache
npm config get prefix
```


### 2. 这两个目录里会生成什么
**`F:\ProgramData\nodejs_package_manager\npm\cache`**
- `_cacache`：npm 的包缓存，按内容哈希存储，不是按包名。
- `_logs`：npm 运行日志。
**`F:\ProgramData\nodejs_package_manager\npm\global`**
- `node_modules`：所有 `npm install -g` 安装的包都放在这里。
- 根目录下直接出现 `.cmd` / `.bat` / `.ps1` 等可执行文件，比如 `tsc.cmd`、`npm.cmd`、`npx.cmd` 等。


### 3. 关键一步：把 global 根目录加入 PATH

因为 Windows 上全局命令的可执行文件就在 `prefix` 的**根下**，所以需要把：

```text
F:\ProgramData\nodejs_package_manager\npm\global
```

加入**系统变量 Path**，而不是用户变量 Path（如果你希望所有用户都能用这些全局命令）。

注意不要写成 `...\global\node_modules`，那样是找不到命令的。




## pnpm

### 独立安装（不依赖nodejs和npm）
官网命令
```powershell
Invoke-WebRequest https://get.pnpm.io/install.ps1 -UseBasicParsing | Invoke-Expression
```

#### 更新
```bash
pnpm self-update
```

#### 卸载
```text
To uninstall, delete C:\Users\Admin\AppData\Local\pnpm, then remove the PNPM_HOME variable and the Path entry pnpm setup added from your user environment variables.
```

### 配置

🛠️ 核心配置命令

|配置类型|执行命令|说明|
|---|---|---|
|**1. 依赖缓存主存储（最重要）**|`pnpm config set store-dir "你的目标路径"`|存放所有项目的共享依赖包。**路径中切勿包含中文**。|
|**2. 全局安装包位置**|`pnpm config set global-dir "你的目标路径"`|存放通过 `pnpm add -g` 安装的全局工具。|
|**3. 全局二进制可执行文件**|`pnpm config set global-bin-dir "你的目标路径"`|存放全局命令的快捷方式（需将此路径手动加入系统环境变量 `Path`）。|
|**4. 状态/缓存数据**|`pnpm config set state-dir "你的目标路径"`|存放 pnpm 运行时的状态记录与元数据。|
配置示例代码
```bash
pnpm config set store-dir "F:\ProgramData\nodejs_package_manager\pnpm\store"
pnpm config set global-dir "F:\ProgramData\nodejs_package_manager\pnpm\global"
pnpm config set global-bin-dir "F:\ProgramData\nodejs_package_manager\pnpm\global\bin"
pnpm config set state-dir "F:\ProgramData\nodejs_package_manager\pnpm\state"
```
验证
```bash
pnpm config list
```
Windows 10 关键环境变量配置
```text
path路径添加可执行文件目录
F:\ProgramData\nodejs_package_manager\pnpm\global\bin
```
全局包安装验证
```bash
pnpm add -g rimraf
rimraf --version
pnpm rm -g rimraf
```



# Rust


# Go

