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

1.创建一个目录  
mkdir Test

2.将当前目录变为git管理仓库  
git init

3.将文件添加到版本库，这里将目录下的所有文件都添加进去了  
git add .

4.告诉git将文件提交到仓库  
git commit -m "first-commit"

5.将当前仓库与远程仓库关联  
git remote add orign 远程仓库的https地址 # eg: git remote add https://github.com/ssmath/Test.git

6.将仓库内master分支的所有内容推送到远程仓库,这里会使用到Github的账号密码  
git push -u orign master

7、创建tag  
git tag 0.1.1

8、查看某个tag信息  
git show 0.1.1

9、将tag推送到服务器  
git push origin --tags 推送所有tag  
git push origin 0.1.1 推送单个tag

10、删除tag  
git tag -d 0.1.1 本地删除tag  
git push origin :refs/tags/0.1.1 远端删除tag  



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

遇到问题3  
[!] The `MGCategoryKit` pod failed to validate due to 1 error:
    - WARN  | summary: The summary is not meaningful.
    - ERROR | [iOS] attributes: Unacceptable type `Hash` for `source_files`. Allowed values: `[String, Array]`.
解决方法  
s.source_files ='MGCategoryKit/Classes/**/*','MGCategoryKit/SubClasses/**/*'  

遇到问题4  
升级组件库时，必须同步更新MGSpecs这个目录  
Example apple$ pod repo push MGSpecs MGCategoryKit.podspec --verbose --allow-warnings  
[!] Couldn't find MGCategoryKit.podspec  
解决方法  
必须在组件库MGCategoryKit目录下执行下面命令  
pod repo push MGSpecs MGCategoryKit.podspec --verbose --allow-warnings 

遇到问题5 库文件都在一个文件夹，无法分层，需求实现class文件夹下面有 categoryFile、 controller、Model、View等目录
解决方法  
修改MGCategoryKit.podspec这个文件
s.subspec 'categoryFile' do |ss|  
    ss.source_files = 'MGCategoryKit/Classes/categoryFile/*'  
  end
  
  s.subspec 'controller' do |ss|  
    ss.source_files = 'MGCategoryKit/Classes/controller/*'  
  end  
  
  s.subspec 'Model' do |ss|  
    ss.source_files = 'MGCategoryKit/Classes/Model/*'  
  end  
  
  s.subspec 'View' do |ss|  
    ss.source_files = 'MGCategoryKit/Classes/View/*'  
  end  
  
  s.source_files ='MGCategoryKit/SubClasses/**/*'  
   s.resource_bundles = {  
     'MGCategoryKit' => ['MGCategoryKit/Assets/*.png']  // 对图片的管理，会生成bundle文件
   }  
   
   对与组件中bundle资源的获取
    NSString *normalImgName = [NSString stringWithFormat:@"%@@2x.png", @"Group"];  
   NSBundle *curBundle = [NSBundle bundleForClass:self.class];  
   NSString *curBundleName = curBundle.infoDictionary[@"CFBundleName"];  
   NSString *curBundleDirectory = [NSString stringWithFormat:@"%@.bundle", curBundleName];  
   NSString *normalImgPath = [curBundle pathForResource:normalImgName ofType:nil inDirectory:curBundleDirectory];  
   imageview.image  = [UIImage imageWithContentsOfFile:normalImgPath];  
