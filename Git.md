## Git

1. #### 安装和使用

   1. ##### git的安装

   2. ##### github 简介

      - Explore：根据兴趣和关注推荐的项目
      - Trending：近期热门

   3. ##### github仓库的概念以及如何创建仓库

      1. readme：介绍项目
      2. gitignore和license
         - gitignore：配置一些你在本地开发时无需上传到远程代码仓库的文件
         - license：证书文件，一般不需添加

2. #### Git 工作流程

   1. 克隆Git资源作为工作目录

   2. 在克隆的资源上编辑、添加或删除文件

   3. 如果其他人修改了，可以更新资源

   4. 在提交前查看修改

   5. 提交修改

   6. 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交

      ![img](../图片/git-process.png)

3. Git 工作区、暂存区和版本库

   工作区：本地里能看到的目录

   暂存区（索引）：stage或index，一般存放在.git目录下的index文件中

   版本库：工作区中有一个隐藏目录.git

   ![img](../图片/1352126739_7909.jpg)

   - objects标识的区域为Git的对象库，实际位于.git/objects目录下，里面包含了创建的各种对象及内容
   - 当对工作区修改的文件执行git add后，暂存区的目录树被更新，同时工作区修改的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中
   - git commit，暂存区的目录树被写到版本库中，master分支会做相应的更新，即master的目录树就是提交暂存区的目录树
   - git reset HEAD，暂存区的目录树会被重写，被master分支执行的目录树所替换，但工作区不受影响
   - git rm --cached <file> ，会直接从暂存区删除文件，工作区则不做出改变
   - git checkout .或者git checkout -- <file>，会用暂存区全部或指定的文件替换工作区的文件，**该操作很危险，会清除工作区中未添加到暂存区的改动**
   - git checkout HEAD. 或者git checkout HEAD <file> ，会用HEAD指向的master命令或者部分文件替换暂存区以及工作区中的文件。**这个命令极具危险，不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动**

4. #### git 创建仓库

   1. **git init**：初始化一个Git仓库，会生成一个.git目录，包含了资源的所有元数据，其他的项目目录保持不变

      ![image-20210506163649741](../图片/image-20210506163649741.png)

   2. **git clone**：从Git仓库中拷贝项目

      - git clone <repo>
      - git clone <repo> <directory> (指定目录)

   3. **git config**：配置

      - 查看 git config --list
      - 编辑 git config -e （针对当前仓库）
      - 设置信息
         - git config --global user.name "xxx"
         - git config --global user.email "xxx"

5. #### Git基础操作

   ![img](../图片/git-command.jpg)

   1. ##### 说明

      - workspace：工作区
      - staging area：暂存区/缓存区
      - local repository：版本库或本地仓库
      - remote repository：远程仓库

   2. ##### 指令

      1. ##### 创建仓库命令

         | 命令      | 说明                   |
         | --------- | ---------------------- |
         | git init  | 初始化仓库             |
         | git clone | 拷贝远程仓库，拉取代码 |

      2. ##### 提交与修改

         | 命令       | 说明                                   |
         | ---------- | -------------------------------------- |
         | git add    | 添加文件到仓库                         |
         | git status | 查看仓库当前的状态，显示有变更的文件   |
         | git diff   | 比较文件的不同，即暂存区和工作区的差异 |
         | git commit | 提交暂存区到本地仓库                   |
         | git reset  | 回退版本                               |
         | git rm     | 删除工作区文件                         |
         | git mv     | 移动或重命名工作区文件                 |

      3. ##### 提交日志

         | 命令             | 说明                                 |
         | ---------------- | ------------------------------------ |
         | git log          | 查看历史提交记录                     |
         | git blame <file> | 以列表形式查看指定文件的历史修改记录 |

      4. ##### 远程操作

         | 命令       | 说明               |
         | ---------- | ------------------ |
         | git remote | 远程仓库操作       |
         | git fetch  | 从远程获取代码库   |
         | git pull   | 下载远程代码并合并 |
         | git push   | 上传远程代码并合并 |

6. #### 对文件的基本操作

7. #### 对分支的基本操作

8. #### git与github深度结合使用

9. 创建代码仓库

   1. 初始化配置

      ```
      git config --global user.name "TongSha"
      git config --global user.email "slxt516@163.com"
      ```

   2. 创建代码仓库：用来保存版本管理，可以还原到某个版本

      ```
      git init
      ```

10. 提交本地代码

   1. 添加指令 add

      ```
      git add readme.txt
      ```

   2. 提交指令 commit

      ```
      git commit -m "Wrote a readme file"
      ```

   3. 查看修改内容 status

      ```
      git status //会提示我们哪些文件发生了改变，但是还没有提交，如果我们想看下具体更改了什么，我们可以用到git diff命令
      git diff
      ```

   4. 查看提交记录

      ```
      git log
      
      /*
      *此次提交对应的版本号
      *提交人：姓名 邮箱
      *提交的时间
      * 提交版本修改的内容：就是我们commit -m "xxx"里的xxx
      */
      ```

   5. 撤销未提交的修改 checkout

      ```
      // 前提未add
      git checkout  src/main/java/com/example/mortgagecalculator/MainActivity.java
      
      // 若已add，先取消添加再撤回提交
      git reset HEAD  src/main/java/com/example/mortgagecalculator/MainActivity.java
      git checkout  src/main/java/com/example/mortgagecalculator/MainActivity.java
      ```

   6. 版本回退：HEAD代表当前版本，上一个版本 HEAD^

      ```
      git reset --hard HEAD
      git reset --hard HEAD^
      git log
      
      // 回复删除的版本
      git reflog 
      git reset --hard xxxxx
      ```

11. 远程仓库

    1. github 介绍

       1. ![img](../../Java/图片/17112209.jpg)

       2. Clone 代码库待本地

          ```
          git clone https://github.com/ZPJay/Garbage.git
          ```

       3. 分支管理

          1. 创建分支：git branch v1.0
          2. 查看版本中所有分支：git branch -a
          3. 切换到某一分支：git checkout v1.0
          4. 删除某一个分支：git branch -D v1.0
          5. 合并分支 git merge v1.0

       4. 本地仓库与远程仓库同步

          1. 同步到远程：git push origin master | git push
          2. 同步到本地：git pull