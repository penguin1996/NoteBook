Git 如何上传本地项目

在 github 上创建一个新的仓库，给它一个合适的名字，比如 NoteBook。
在本地创建一个文件夹，用来存放你的项目文件，比如 NoteBook。
在本地文件夹中打开 git bash，输入 git init 命令，初始化一个本地仓库。
将你的项目文件复制或移动到本地文件夹中，然后输入 git add . 命令，将所有文件添加到暂存区。
输入 git commit -m "first commit" 命令，将暂存区的文件提交到本地仓库，并添加一个提交信息。
输入 git remote add origin https://github.com/penguin1996/NoteBook.git 命令，将本地仓库与远程仓库关联起来，其中 penguin1996是你的 github 用户名，NoteBook 是你的 github 仓库名。
输入 git push -u origin main命令，将本地仓库的内容推送到远程仓库的 main分支，并设置为默认分支。
这时你可以在 github 上查看你的仓库，应该能看到你的项目文件已经上传成功了。



echo "# NoteBook" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/penguin1996/NoteBook.git
git push -u origin main

git remote add origin https://github.com/penguin1996/NoteBook.git
git branch -M main
git push -u origin main



# OpenSSL SSL_read: Connection was reset, errno 10054问题

使用命令：git config --global https.sslVerify "false" 



参考：

https://blog.csdn.net/m0_63526347/article/details/130414871