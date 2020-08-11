# MGMainProject
主工程

参考文章
https://www.jianshu.com/p/6ee3e8a50d47
https://www.jianshu.com/p/f903ecf8e882
https://cloud.tencent.com/developer/article/1398152

git问题
https://blog.csdn.net/xieneng2004/article/details/81044371

vim命令
https://www.cnblogs.com/dalaoban/p/9381305.html

如何推送本地工程到远程仓库
# 步骤
# 1.创建一个目录
mkdir Test
# 2.将当前目录变为git管理仓库
git init
# 3.将文件添加到版本库，这里将目录下的所有文件都添加进去了
git add .
# 4.告诉git将文件提交到仓库
git commit -m "first-commit"
# 5.将当前仓库与远程仓库关联
git remote add orign 远程仓库的https地址 # eg: git remote add https://github.com/ssmath/Test.git
# 6.将仓库内master分支的所有内容推送到远程仓库,这里会使用到Github的账号密码
git push -u orign master


遇到问题1
! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/miaohy/MGMainProject.git'
解决方法 
git pull origin master --allow-unrelated-histories //把远程仓库和本地同步，消除差异

遇到问题2
[!] An unexpected version directory `Classes` was encountered for the `/Users/apple/.cocoapods/repos/miaohy/MGCategoryKit` Pod in the `MGCategoryKit` repository.
解决方法
source 'https://github.com/miaohy/MGSpecs.git'
#这里不是每一个组件的地址，而是整个组件的地址
