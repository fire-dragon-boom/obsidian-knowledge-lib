# 设置新文件位置
## 1. 设置命令

```bash
npm config set cache "F:\ProgramData\nodejs_package_manager\npm\cache"
npm config set prefix "F:\ProgramData\nodejs_package_manager\npm\global"
```

执行后，可以用下面命令确认是否写入成功：

```bash
npm config get cache
npm config get prefix
```


## 2. 这两个目录里会生成什么
**`F:\ProgramData\nodejs_package_manager\npm\cache`**
- `_cacache`：npm 的包缓存，按内容哈希存储，不是按包名。
- `_logs`：npm 运行日志。
**`F:\ProgramData\nodejs_package_manager\npm\global`**
- `node_modules`：所有 `npm install -g` 安装的包都放在这里。
- 根目录下直接出现 `.cmd` / `.bat` / `.ps1` 等可执行文件，比如 `tsc.cmd`、`npm.cmd`、`npx.cmd` 等。


## 3. 关键一步：把 global 根目录加入 PATH

因为 Windows 上全局命令的可执行文件就在 `prefix` 的**根下**，所以需要把：

```text
F:\ProgramData\nodejs_package_manager\npm\global
```

加入**系统变量 Path**，而不是用户变量 Path（如果你希望所有用户都能用这些全局命令）。

注意不要写成 `...\global\node_modules`，那样是找不到命令的。


