# 版本控制系统 svn \ git  
 （  1. 可以记录不同版本变化  ；  2. 方便多人协作使用 ）
1.   svn 集中化版本控制系统   全量部署，增量变化 ( 反向计算增量很麻烦，且不方便计算机计算处理 )  =====》 记录不同版本变化 （需要联网，且速度慢）
2.   git 分布式版本控制系统    全量部署，全量变化 （不需要联网也可以，且速度快） --方便团队协作开发

### window支持exe格式，而linux不支持该格式

### git支持一些linux和window指令（创始人是linus的）

### 电脑自带的终端cmd对一些脚手架的效果更好（相对于git自带的来说，对这些脚手架的效果）



# git 指令（使用方法查手册/文档）
### git的工作模式
【 working directory工作目录 ---> staging area (index)暂存区(作用:为文件创建索引,方便查找,进行分类) ---> repository git本地仓库(到了本地仓库，才叫做一个版本) 】
工作目录 ==== 》 暂存区 ==== 》 本地仓库 ===== 》 远程仓库github/gitee...
### 配置相关信息 
1. $ git config --global user.name 名字
2. $ git config --global uaer.email 邮箱
3. $ git config --list （查看相关配置信息）
### 初始化(本地仓库)
1. $ git init (初始化本地仓库) --产生master分支 (主线分支) 
2. $ rm -rf .git (强制删除本地仓库，仓库名为.git) ---> 删库跑路

### git操作
   
【 working directory工作目录 ---> staging area (index)暂存区(作用:为文件创建索引,方便查找,进行分类) ---> repository git本地仓库(到了本地仓库，才叫做一个版本) 】
1. $ git add index.html index.css (添加index.html和index.css到缓存区 --前提是index.html\index.css要已经保存才行) ===》 （该步骤的目的：为添加进来的文件创建索引，以及通过索引给文件分类，方便存储和查找）
2. $ git commit -m 'project init' (提交版本(project init 版本名 -- (注释说明用的))到本地仓库)
3. $ git add . / $ git add *(添加所有文件到暂存区)
4. $ git status (查看(文件)当前状态 --执行到哪一步)
5. $ git checkout -- index.html (撤销工作区修改的操作,(对于仅在工作目录上改变的文件) 使得当前的index.html恢复到上一个版本的状态)  -- > 真正的用处在于切换分支
6. $ git log (查看诺干个版本提交的信息--完整版)
7. $ git log 还能做内容更新
8. $ git log --graph (图形化展示诺干个版本提交信息)
9. $ git reflog (查看历史记录 -- 简化版) -- > (记录版本信息) ---> (获取SHA-1加密算法得到的每个版本的唯一钥匙)
10. $ git diff (比较工作区与暂存区的差异)
11. $ git diff -- cached (比较暂存区与本地版本库中最近一次commit的内容差异)
12. $ git diff HEAD (比较工作区与本地版本库中最近一次commit的内容)
13. $ git diff <commit-id> <commit-id> (比较俩个commit之间的差异) 输入的是每一个版本经过SHA-1散列加密算法（美国安全局提出）得到的字符串
14. $ git reset HEAD index.html (暂存区文件撤销，不覆盖工作区)
15. $ git reset --hard HEAD (切换版本/ 回退版本)(HEAD头指针:记录当前版本)
16. $ git reset --hard HEAD^ (当前版本回退一个版本)
17. $ git reset --hard HEAD~n (当前版本回退n个版本)
18. $ git reset --hard commitId (切换到某个版本)
19. --hard(回退全部--包括HEAD\index\working tree)   --mixed(回退部分--包括HEAD,index)   --soft(只回退HEAD)
20. $ git commit --amend (往当前版本追加内容,严格来说是创建一个新的版本，但是与当前的版本内容一致，并往里头追加新内容) ==> (同时,会进入该版本的区域,按esc退出:wq) ==> linux指令
    #### 分支，多人协作必备（一个项目一个库）
21. $ git branch 分支名 (创建分支)
22. $ git checkout 分支名 （切换到不同分支）
23. $ git checkout -b 分支名 （创建并切换到该分支上去）
24. $ git stash (创建一个临时存放区，将当前修改的存进去，以便在不进行提交到暂存区/新版本、不创建新分支的情况下，可以切换到别的分支/版本，而保留修改的信息)
25. ps：没有提交版本，跨分支都是不合理的；（除非用$ git stash 存起来） -----》 吐出来 ----》 $ git stash pop
26. $ git merge 分支名 （将当前分支与代码填写的分支进行合并）--- 有冲突会提示，没冲突直接完成合并
27. $ git branch 查看分支

### 远程控制
1. ssh-keygen生成一个密钥 （用于识别连接本地仓库与远程仓库）--在本地电脑用户文件夹下，找到密钥，并在github上设置好
2. $ git remote add 远程仓库名（别名） 远程仓库地址（https/ssh）--添加一个远程仓库连接
3. $ git push 远程仓库名 分支名(master) --将本地仓库的内容放到远程仓库的某个分支上
4. ps：尽量不要跨分支操作，（master一般作为主线分支，需要加密保护，是要上线的）
5. $ git pull 远程仓库名 分支名    （拉取该远程仓库的该分支的所有数据，到本地仓库上来，用于每天确保操作的代码与服务器上的保持一致）
6. $ git clone ssh (用于下载别人的代码)
7. cd ..是返回上一层目录， cd -是返回到上一次的工作目录。
8. $ git rm -r --cached 路径 (删除暂存区中该路径下的内容)
9. .gitignore文件是配置文件
10. learn git branching 学习的网站名
