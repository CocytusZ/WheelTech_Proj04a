# Git Upload files

1. git clone branch 到本地
   
2. 查看本地分支
```{.sh}
git branch
```

3. 切换本地分支
```{.sh}
git checkout <分支名>
Git
# e.g.
git checkout main
```

4. 复制文件到本地文件夹

5. 上传到本地Reposity
```{.sh}
git add . #加当前文件夹下所有文件
git commit -m "备注_必填"
```

6. 推到当前远程仓库子分支
```
git push origin <主分支名>/<子分支名>

#e.g.
git push origin main:yao_thinkpad
```