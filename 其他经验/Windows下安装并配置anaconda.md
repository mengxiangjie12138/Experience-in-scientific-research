1.下载anaconda

官方下载地址：https://www.anaconda.com/download/

清华源下载地址：https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

2.安装anaconda

一直选择下一步即可，只有一处注意的地方。

这里两个选项都需要选择，因为要添加到系统变量里（后续自己配置系统变量会很麻烦，所以在这里直接配置好。）

cmd指令输入conda -V，得到conda版本，验证anaconda安装成功。(如未添加环境变量，则无法查看版本)cmd命令行输入 python，输出当前python版本为3.7，接下来新建python3.6。
注：cmd中退出Python编辑为输入Control +Z ,按回车。

3.新建python环境

cmd指令下输入:conda create -n [自取环境名字] python=3.6

cmd下输入activate [python环境名字] 用以激活python环境

4.更新下载源

cmd命令：conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 下载源变为清华镜像源。