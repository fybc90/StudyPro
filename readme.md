学习git
=====
* ####Git是什么
	Git是目前世界上最先进的分布式版本控制系统

* ####SVN与Git的区别

	SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了

	Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

* 安装

	安装 Git 版本控制工具 [点击下载](https://git-for-windows.github.io/)

* 配置

	`git config --global user.name "fybc90"`
    `git config --global user.email "fybc90@163.com"`
    因为Git是分布式版本控制系统，所以需要填写用户名和邮箱作为一个标识
    **注意：**git config  –global 参数，有了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然你也可以对某个仓库指定的不同的用户名和邮箱。

* 操作

	1.创建版本
	`cd D:`   `mkdir study`   `cd study`
    和windows中cmd的命令一样 进入d盘、创建文件夹study、进入study文件夹；
    `git init` 把当前目录变成git可以管理的仓库。

	2.显示当前的目录
	`pwd`

	3.把文件添加暂存区
	`git add readme.md` 【git add 文件名】把文件添加到暂存区中。

	3.把文件提交到仓库
	`git commit -m "readme.md"` 【git commit -m "文件名"】

	4.查看状态
	`git status`

	5.查看日志
	`git log` 查看历史记录 提交人(用户名、邮箱) 和提交时间
    `git log --pretty==online` 简单形式的历史记录只列出版本号及提交备注
    `git reflog` 查看全部日志

	6.查看变更
	`git  diff readme.md` 【git diff 文件名】 可以列出文件修改内容

	7.版本回退/回滚
	`git reset --hard HEAD^` 回退到上一个版本
    `git reset --hard HEAD^^`回退到上上个版本
    `git reset --hard 7acf209`【git reset --hard 版本号】此版本号使用`git reflog`查看

	8.查看文件内容
	`cat readme.md` 【cat 文件名】列出文件文本内容

	9.撤销修改/还原
	`git checkout -- readme.md` 【git checkout -- 文件名】 这里的文件名好像区分大小写；只能撤销未添加到暂存区的内容，即没有执行`git add`命令。

	10.删除文件
	`rm readme.md`  or `git rm readme.md`【rm 文件名】在文件的目录下执行，和windows下的cmd命令一样。

    11.恢复删除的文件
	删除文件后没有提交：`git checkout -- readme.md`
    删除文件并提交就只能版本回滚【见7】，

* 远程仓库

	1.创建SSH Key
	在用户主目录下“C:/User/username"查看是否含有.ssh目录和目录下是否含有id_rsa和id_rsa.pub文件。有则跳过；没有则执行如下命令`ssh-keygen-t rsa -C "fybc90@163.com"`。id_rsa是私钥，id_rsa.pub是公钥。

	2.注册Github账号
	注册登陆[Github](http://Github.com);【Setting】 -> 【SSH Keys】 -> 【Add SSHkey】;起一个有意义的Title，将id_rsa.pub的文本内容复制到【Key】中，点击【Add Key】

	3.如何添加远程库
	+ 【New repository】-> 填写你的仓库名称 -> 【Create repository】;
    + 现在需要将本地仓库与远程仓库关联`git remote add origin https://github.com/fybc90/stydy.git`;
    + 把本地库推送到远程`git push -u origin master`由于远程库是空的，我们第一次推送master分支时，加上`-u`参数，Git不但会把本地的master分支内容推送到远程新的master分支，还会把本地的master分支和远程的mater分支关联起来，在以后的推送或者拉取的时就可以简化命令`git push origin master`由于第一次推送还需输入github的用户名和密码。

	4.从远程库克隆
	`git clone https://github.com/fybc90/study` 在需要克隆目的目录下执行

    5.创建和合并分支
    `git checkout -b dev` 【git checkout -b 分支名称】
    6.删除分支