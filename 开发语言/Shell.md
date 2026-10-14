# 知识点

## 循环目录
``` shell
# 开启显示隐藏文件ex: .c.txt
shopt -s dotglob

for file in ~/*;do

echo "$file"

done

shopt -u dotglob

```

# 特性
1. 会将命令输出的内容，存放到一个临时的虚拟文件中，实际上执行的是 ==`bash file`==
```bash
bash <(命令)
```
