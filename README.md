# mrliuwinter.github.io
个人博客

hexo分支存放的是博客源代码
master分支存放的是生成的静态文件

先设置用户名密码
2. git config --global user.email "你的邮箱"
3. git config --global user.name "你的github用户名"

生成秘钥： ssh-keygen -t rsa -C "xxx@xxx.com"

hexo init  #初始化仓库（仓库名要与博客名字一致）

git init  #git初始化

# 与远程 Git 仓库建立连接，只此一次即可
git remote add origin https://github.com/你的用户名/你的名字.github.io
**注：origin不是仓库源时要再执行一次**

git checkout -b hexo #切换分支，所有的提交是在hexo分支下完成的（存放的是源代码）

git push --set-upstream origin hexo #设置默认提交hexo分支

$ git pull origin hexo --allow-unrelated-histories 

#允许不同历史版本合并，先pull远程仓库版本，合并之后，再push同步版本

