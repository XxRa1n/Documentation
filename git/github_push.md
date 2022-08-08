### Github push

步骤：

1. git本地建库
2. git remote add origin git@github.com:githubusername/repoName.git
   origin是默认远程库的名字，可以更改
3. 添加SSH key。
   输入ssh-keygen -t rsa -C "githubusername"生成id_rsa.pub等文件
   将id_rsa.pub文件中的内容复制到github->setting->SSH and GPG keys中
4. git push -u origin master
   "-u"参数会将本地库与github库关联起来
   下载推送的时候可以直接：
   git push origin master