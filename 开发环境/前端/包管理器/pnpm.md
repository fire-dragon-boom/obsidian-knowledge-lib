# 设置新文件位置

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




# 问题
## 问题1
> [ERR_PNPM_IGNORED_BUILDS] Ignored build scripts: esbuild@0.27.3, esbuild@0.27.7, sharp@0.34.5, workerd@1.20260310.1, workerd@1.20260515.1
> 
> pnpm 会在pnpm i 的时候阻止不信任的  build scripts，并且会生成一个文件进行配置 pnpm-workspace.yaml

```bash
#Run "pnpm approve-builds" to pick which dependencies should be allowed to run scripts.
pnpm approve-builds
```
```yaml
allowBuilds:
  esbuild: true
  sharp: true
  workerd: true
```




