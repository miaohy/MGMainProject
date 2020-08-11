# MGMainProject
主工程

参考文章
https://www.jianshu.com/p/6ee3e8a50d47
https://www.jianshu.com/p/f903ecf8e882

git问题
https://blog.csdn.net/xieneng2004/article/details/81044371

vim命令
https://www.cnblogs.com/dalaoban/p/9381305.html


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
