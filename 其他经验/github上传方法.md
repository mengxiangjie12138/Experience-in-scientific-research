## 普通文件上传

1.下载[Git](https://link.jianshu.com/?t=https://git-scm.com/downloads)（后续操作在Git Bush中完成）

2.绑定用户名和邮箱

```csharp
$ git config --global user.name "hanyuntao"
$ git config --global user.email "hanyuntaocn@163.com"
```

3.初始化本地仓库

```
$ git init
```

4.将所有文件添加到仓库

```
$ git add .
```

5.提交文件。双引号内是提交注释。

```
git commit -m "提交文件"
```

6.关联Github仓库（先到GitHub中复制仓库http地址，再填入Git Bush中）

```
$ git remote add origin https://github.com/hanyuntao/text.git
```

7.上传本地代码

```
$ git push -u origin master
```

## 超过100M的大文件上传（LFS）

1.下载安装[LFS](https://git-lfs.github.com/)

2.运行LFS

```
$ git lfs install
```

3.更新本地仓库

```
$ git pull origin master
```

4.使用 Git LFS 管理托管文件

```
$ git lfs track "*.pdf"
```

5.追踪文件 `.gitattributes`

```
$ git add .gitattributes
```

6.后续步骤和普通文件上传一样，但注意大文件需要单个上传，add时不能添加其他文件。

















