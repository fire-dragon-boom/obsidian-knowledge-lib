
## 问题
### 问题1
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




