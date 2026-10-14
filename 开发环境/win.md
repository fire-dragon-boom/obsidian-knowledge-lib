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

pnpm 的配置逻辑和 npm 不太一样，它把“缓存”和“全局包”的概念做了更细的拆分。结合你之前的路径规划，可以这样设置：

### 对应你规划路径的 pnpm 配置

pnpm 没有直接对应 npm `cache` 的单一选项，它的核心是 **`store-dir`**（存储所有包内容的地方，相当于更底层的缓存），以及 **`global-dir`** 和 **`global-bin-dir`**（分别管全局包的 node_modules 和可执行文件）。

参考你的路径，可以这样映射：

| 你的 npm 路径        | 对应的 pnpm 配置项     | 建议的 pnpm 路径                                             |
| :--------------- | :--------------- | :------------------------------------------------------ |
| `...\npm\cache`  | `store-dir`      | `F:\ProgramData\nodejs_package_manager\pnpm\store`      |
| `...\npm\global` | `global-dir`     | `F:\ProgramData\nodejs_package_manager\pnpm\global`     |
| （无直接对应，但需要）      | `global-bin-dir` | `F:\ProgramData\nodejs_package_manager\pnpm\global\bin` |

### 设置命令

和 npm 一样，用 `pnpm config set` 来写入配置：

```bash
pnpm config set store-dir "F:\ProgramData\nodejs_package_manager\pnpm\store"
pnpm config set global-dir "F:\ProgramData\nodejs_package_manager\pnpm\global"
pnpm config set global-bin-dir "F:\ProgramData\nodejs_package_manager\pnpm\global\bin"
```

**需要留意**：`global-bin-dir` 是 pnpm 用来存放 `tsc`、`vite` 这类全局命令可执行文件的地方。你需要把这个 `bin` 目录（而不是 global 根目录）加到**系统变量 Path** 里。

### 关于“对所有用户生效”

和 npm 的情况类似，`pnpm config set` 默认只写入当前用户的配置文件（Windows 上通常在 `~/AppData/Local/pnpm/config/rc` 或 `.npmrc`），只对当前用户生效。

如果你想对所有用户生效，有两种更稳妥的方式：

1.  **设置系统环境变量**：创建 `PNPM_HOME` 系统变量，指向 `F:\ProgramData\nodejs_package_manager\pnpm\global`。pnpm 很多路径（尤其是 `global-bin-dir`）会基于它来计算。
2.  **使用 `--global` 标志**：执行 `pnpm config set <key> <value> --global`。不过要注意，pnpm 的全局配置文件位置可能随版本变化，升级时不如环境变量稳定。

### 一个重要的版本差异

pnpm v11 调整了全局命令的存放策略：现在全局安装的二进制文件会放在 `PNPM_HOME` 下的 **`bin` 子目录**里，而不是直接放在 `PNPM_HOME` 根下。所以如果你用的是较新版本，记得把 `...\pnpm\global\bin` 这个路径加进 Path。




# Rust


# Go

