## git 基础
### diff and patch 是版本控制的起源
#### diff: diff 用来比较两个文件或者目录之间的差异
```
diff -u left.c right.c
```
#### patch： patch是diff的反向操作
```
patch left.c diff.txt
```

### 过去的version control tools

#### RCS: 最早期的本地版本控制工具
#### CVS & SVN : 集中式版本控制工具
![[Pasted image 20240405002835.png]]
		
#### Git
![[Pasted image 20240405003034.png]]
Git 是分布式，除了第一版是记录全部，其他都是记录差异
![[Pasted image 20240405003319.png]]

#### Git vs SVN
![[Pasted image 20240405003619.png]]

### git summary
high speed, simple design, 非线性开发，完全分布式，高效管理
![[Pasted image 20240405003945.png]]
### git 配置
![[Pasted image 20240405004145.png]]

![[Pasted image 20240405004208.png]]![[Pasted image 20240405004451.png]]![[Pasted image 20240405004456.png]]
![[Pasted image 20240405004600.png]]
![[Pasted image 20240405004651.png]]
### git 基本命令
![[Pasted image 20240405233301.png]]

![[Pasted image 20240405233442.png]]
![[Pasted image 20240405233705.png]]
#### git add & git rm & git mv

#### git status 
命令用于显示工作目录和暂存区的状态

#### git commit 
主要是将暂存区里的文件改动提到到本地的版本库
git commit file_name -m "commit message"

#### git log 
用于查看提交历史

#### git push origin branch_name
![[Pasted image 20240406000934.png]]

#### 分支管理 - git branch & git checkout 
git branch 命令 可查看 本地工程的所有git 分支名称
git branch -r 看远端服务器上的哪些分支
git branch -a 看远端服务器和本地工程所有的分支

git checkout -b new_branch_name 和 git branch  branch_name 都可以用于新建分支

git branch 新建分支后并不会切换到新分支
git checkout -b 新建分支后会自动切换到新分支

git branch -d 
git branch -D 强制删除

git branch -d -r branch_name 删除服务器上的远程分支

git checkout branch_name
git pull 的作用是，从远端服务器中获取某个分支的更新，再与本地指定的分支进行自动合并。
git pull origin remore_branch:local_branch 常用的切换分支命令
git pull origin remote_branch

分支管理
git fetch 的作用是，从远端服务器中获取某个分支的更新到本地仓库。

git pull 作用是，从远端服务器中获取分支的更新，与本地的分支进行自动合并
![[Pasted image 20240406003019.png]]

#### git merge
git merge branch_name指定分支合并到当前分支


#### git rebase 
git rebase 也可以合并目标分支到当前

#### git reset 撤销
git reset commit_id
git reset --mixed/hard/soft

git checkout . 用于回退本地所有修改未提交的文件内容 谨慎使用

### 本地基本提交推送
#### 比较 git diff
git diff 分支名 origin/分支名

git fetch  + git merge = git pull

### 撤销
git log
git reset --hard xxxxxxx
git push origin ...


如果没有提交 然后回退
git checkout <文件名> 可以还原这个文件的内容

git checkout . 还原所有 ，一下就回去了

git reflog 可以看看之前有什么改动 没有提交

## Idea
![[Pasted image 20240413222309.png]]
![[Pasted image 20240413222321.png]]


![[Pasted image 20240413222725.png]]
![[Pasted image 20240413223023.png]]

## SQL


## Linux


## Java
### Javs基本数据类型及应用
primitive types: 
	数值 整数，浮点
	字符型 char
	布尔型 bool
	![[Pasted image 20240414112611.png]]
![[Pasted image 20240414112715.png]]
基本数据类型在使用时，如忽略range，会异常
浮点数不能==作比较，因为浮点转换成二进制后，由于精度问题，会计算偏差

![[Pasted image 20240414115801.png]]

#### 字符转换
	自动类型转换：整型到浮点还是可能出现精度损失
	强制类型转换
	类型提升
		![[Pasted image 20240414115939.png]]

		提升规则：
		当表达式包含多个基本类型的值
			byte char short 自动提升至int
			表达式的类型自动提升至表达式中最高数据类型
			
#### 引用数据类型
在堆内存中，类似C的指针，引用类型存放的是对象的引用
![[Pasted image 20240414120741.png]]
##### 包装类：

![[Pasted image 20240414120952.png]]
![[Pasted image 20240414121058.png]]
![[Pasted image 20240414121150.png]]
![[Pasted image 20240414121242.png]]
### 基本语法
#### Java 的程序结构
不同的包组成，包下面有java文件，包括 包声明，import声明，公共类/接口
![[Pasted image 20240417224918.png]]
![[Pasted image 20240417225905.png]]
![[Pasted image 20240417230058.png]]
![[Pasted image 20240417230224.png]]
![[Pasted image 20240417230235.png]]
![[Pasted image 20240417235344.png]]
![[Pasted image 20240418004508.png]]
![[Pasted image 20240418005139.png]]

### Lamda表达式
### IO programming
![[Pasted image 20240418005301.png]]
![[Pasted image 20240418005732.png]]![[Pasted image 20240418005749.png]]
![[Pasted image 20240418005951.png]]
![[Pasted image 20240418010050.png]]
![[Pasted image 20240418010106.png]]
### regExp
![[Pasted image 20240418010638.png]]

![[Pasted image 20240418010845.png]]
![[Pasted image 20240418012134.png]]

D 代表所有字母的
d+ 表示至少一个数字
.* 表示任何字符串

![[Pasted image 20240418011227.png]]
净化：就是把匹配标志可能替换成安全字符

![[Pasted image 20240418011608.png]]
### OOP

## 程序员的一天
1、需求串讲
2、需求分析
	文档- task： 例如登录，1. unit test 2. page UI 3. Interface 4.前后端的重构
3、软件设计
	分解问题-模式识别-抽象化-算法
4、代码提交
![[Pasted image 20240418012536.png]]