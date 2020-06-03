正确步骤：
 //初始化仓库
1. git init

//添加文件到本地仓库
2. git add .(文件name) 

//添加文件描述信息
3. git commit -m "first commit" 
远程仓库地址 //链接远程仓库，创建主分支
4. git remote add origin "https://gitee.com/youtname/vscode.git" 


**(注意:先pull后push)**
 // 把本地仓库的变化连接到远程仓库主分支
// 这句代码是在git 2.9.2版本发生的，最新的版本需要添加 --allow-unrelated-histories 告诉 git 允许不相关历史合并
5. git pull origin master --allow-unrelated-histories
 //把本地仓库的文件推送到远程仓库
6. git push -u origin master