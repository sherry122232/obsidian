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
查询数据的限制和排序
order by name, age DESC 先name升序，再age降序

#### 单行函数
##### 字符串
concat（”“,""）
substr('',1,5) 取子串
length
instr
![[Pasted image 20240420182128.png]]
##### 数字：
![[Pasted image 20240420182239.png]]
##### date：
![[Pasted image 20240420182248.png]]
##### 转换：
![[Pasted image 20240420182340.png]]
![[Pasted image 20240420182352.png]]
![[Pasted image 20240420182436.png]]
![[Pasted image 20240420182446.png]]
![[Pasted image 20240420182521.png]]

#### 分组函数
```
avg
sum
count
max
min

// groupby
// having need to be used with groupby
// 分组函数可以嵌套

```
![[Pasted image 20240420185137.png]]

#### 多表查询
1. 种类
		- 自连接
		- 等值连接
		- 外连接
			- 左外连接 
			- 右外连接
			- 全连接
#### sql optimization
- avoid using * , 使用列名
- 使用别名
- where 子句中的链接顺序，尽量将能缩小范围的放在右边
- 使用>= instead of >
- using truncate instead of delete
	- delete 没有commit操作，回滚中会有删除操作回复的信息
	- truncate 就没有以上
- 尽量多use commit
- 不要在索引列使用函数
	- 例如 where sal*2>20 不好，应该where sal > 20/2


#### 子查询介绍 - 嵌套查询
在查询时基于位置是应考虑使用子查询
子查询必须包含在括号类
将子查询放在右侧
单行子查询用单行运算符，多行用多行运算符

种类
	- 单行子查询： 结果只有一行的。> < = >= <= <>
	- 多行子查询:  in, any, all
	- 空值子查询
	```
	```
```
select emp, ename, jpb, sal
from emp
where empno in ()
```

#### 数据操作语句 - DML
##### insert 
	- ![[Pasted image 20240420191414.png]]
- ![[Pasted image 20240420191514.png]]
- ![[Pasted image 20240420191520.png]]
##### update
![[Pasted image 20240420191644.png]]

##### delete 
delete from table where ...

#### 表结构的操作语句
![[Pasted image 20240420194817.png]]
![[Pasted image 20240420194830.png]]

![[Pasted image 20240420195014.png]]

![[Pasted image 20240420195842.png]]
![[Pasted image 20240420195847.png]]
![[Pasted image 20240420200027.png]]
![[Pasted image 20240420200125.png]]![[Pasted image 20240420200148.png]]
#### 事务操作语句

事务开始 - 第一个DML 语句开始
事务结束 - 发出commit 或者 rollback 
		或者DDL或者DCL语句执行 （隐式提交
		用户退出iSQL*PLus
		系统崩溃

控制事务的命令
- commit 命令
- rollback命令，撤销
- savepoint/rollback to savepoint
## Linux

### linux intro
![[Pasted image 20240421002932.png]]

常见操作系统：dos,windows, unix, linux, mac os, android, ios
linux 是开源的，linux占用内存小，面向开发者。windows是面向消费者。
linux是一套免费试用和自由传播的类unix操作系统。可以管理计算机的所有硬件资源，进行cpu调度。

redhat,centos, suse: 发行版os，侧重网络服务 管理
debian ubuntu 红旗，社区类。侧重用户体验。

#### linux结构
- 应用程序
- shell 程序： bourne shell(sh), C shell 和 korn shell, bash shell(/bin/bash)
- linux 内核kernel
- 硬件系
-![[Pasted image 20240421003332.png]]

#### 特点
![[Pasted image 20240421003403.png]]
#常用远程接入工具: xshell xftp
#### 目录结构
![[Pasted image 20240421003635.png]]
### linux 用户管理
![[Pasted image 20240429133144.png]]

1.2 etc/password 结构
1.3 文件结构
![[Pasted image 20240429133301.png]]
![[Pasted image 20240429133340.png]]
![[Pasted image 20240429133415.png]]

![[Pasted image 20240429133421.png]]

![[Pasted image 20240429133441.png]]

![[Pasted image 20240429133620.png]]
![[Pasted image 20240429133843.png]]
![[Pasted image 20240429133905.png]]
![[Pasted image 20240429133915.png]]
![[Pasted image 20240429133922.png]]
![[Pasted image 20240429133936.png]]

#### 文件和目录管理

绝对路径和相对路径。

pwd: 显示当前工作目录
cd: 更改工作目录

![[Pasted image 20240430232644.png]]

![[Pasted image 20240430232929.png]]
![[Pasted image 20240501164639.png]]

2.3.2 修改群组
![[Pasted image 20240501164652.png]]

2.3.3 修改权限
![[Pasted image 20240501164744.png]]

#### 新建文件 touch ...
#### 新增目录 mkdir
![[Pasted image 20240501164846.png]]
#### 复制文件或者目录
![[Pasted image 20240501164917.png]]
![[Pasted image 20240501165025.png]]

#### 复制文件或者目录
![[Pasted image 20240501165032.png]]
#### 删除 rmdir 
![[Pasted image 20240501165116.png]]
![[Pasted image 20240501165144.png]]

#### 3.5 查找文件或者目录路径
![[Pasted image 20240501165343.png]]
#### 3.6 查看文件内容
![[Pasted image 20240501165324.png]]
3.7 查找
![[Pasted image 20240501165753.png]]
#### 管道
![[Pasted image 20240501165840.png]]
#### 输出重定向
![[Pasted image 20240501165951.png]]
### vim

#### 三种模式
![[Pasted image 20240501172016.png]]
#### 一般模式
![[Pasted image 20240501172054.png]]
![[Pasted image 20240501172127.png]]
![[Pasted image 20240501172216.png]]
![[Pasted image 20240501172300.png]]
![[Pasted image 20240501172402.png]]

### linux文件系统
#### 简介
![[Pasted image 20240501174033.png]]
#### 分类
![[Pasted image 20240501174122.png]]
非索引文件系统，只有block存在，需要一个一个block的读，效率低。
索引式![[Pasted image 20240501174302.png]]
#### 目录树的读取
![[Pasted image 20240501174349.png]]
### linux的磁盘分区介绍
2.1 分区类型
![[Pasted image 20240501174458.png]]
![[Pasted image 20240501180425.png]]

![[Pasted image 20240501183336.png]]

![[Pasted image 20240501183343.png]]
![[Pasted image 20240501183353.png]]
![[Pasted image 20240501183409.png]]
![[Pasted image 20240501183420.png]]
![[Pasted image 20240501183426.png]]
![[Pasted image 20240501183439.png]]
![[Pasted image 20240501183501.png]]

![[Pasted image 20240501182315.png]]
![[Pasted image 20240501182320.png]]

### linux 网络管理
![[Pasted image 20240501183626.png]]
![[Pasted image 20240501183747.png]]
![[Pasted image 20240501183904.png]]
![[Pasted image 20240501183935.png]]

![[Pasted image 20240501190143.png]]
![[Pasted image 20240501190158.png]]

![[Pasted image 20240501190206.png]]
![[Pasted image 20240501190234.png]]
![[Pasted image 20240501191452.png]]
![[Pasted image 20240501191500.png]]

![[Pasted image 20240501191519.png]]

### linux 进程管理和服务管理
![[Pasted image 20240501192643.png]]
![[Pasted image 20240501192725.png]]

![[Pasted image 20240501192732.png]]
![[Pasted image 20240501192747.png]]
![[Pasted image 20240501203613.png]]
![[Pasted image 20240501203625.png]]
### 任务管理
![[Pasted image 20240501203643.png]]
![[Pasted image 20240501203652.png]]
![[Pasted image 20240501203659.png]]

![[Pasted image 20240501203709.png]]
![[Pasted image 20240501203724.png]]
![[Pasted image 20240501203729.png]]
![[Pasted image 20240501203738.png]]
![[Pasted image 20240501203748.png]]
![[Pasted image 20240501203801.png]]
### linux 系统监控
![[Pasted image 20240501203838.png]]
![[Pasted image 20240501203846.png]]
![[Pasted image 20240501203916.png]]
![[Pasted image 20240501203934.png]]
![[Pasted image 20240501203943.png]]
![[Pasted image 20240501203950.png]]
![[Pasted image 20240501204416.png]]
![[Pasted image 20240501204434.png]]

![[Pasted image 20240501204444.png]]

![[Pasted image 20240501204455.png]]
![[Pasted image 20240501204511.png]]
### 查看登录信息
![[Pasted image 20240501204541.png]]
![[Pasted image 20240501204547.png]]![[Pasted image 20240501204557.png]]
![[Pasted image 20240501204609.png]]
### 温故
![[Pasted image 20240501205043.png]]
![[Pasted image 20240501205051.png]]

![[Pasted image 20240501205506.png]]
![[Pasted image 20240501205545.png]]
![[Pasted image 20240501205927.png]]

## Java
### Java基本数据类型及应用
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
判断，不要通过浮点类型。
![[Pasted image 20240616225531.png]]
![[Pasted image 20240616230057.png]]
##### 拆装箱
![[Pasted image 20240616230349.png]]
![[Pasted image 20240616230722.png]]
在-128-127范围内的话 用==是对的。用equals是相同的。因为这里都是对象。
### dsds 
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
#### 运算符
![[Pasted image 20240616235728.png]]
![[Pasted image 20240616235858.png]]
![[Pasted image 20240617000125.png]]
 ![[Pasted image 20240617000136.png]]
 ![[Pasted image 20240617000154.png]]
 
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

### 数据转换

![[Pasted image 20240520171252.png]]

## OOP

```
class 
特征（属性attribute）
功能（方法method）

// 做一道菜，红烧排骨
// 类：菜，对象：排骨

// 创建对象的语法
// new 类名（）;
```

```
package chapter04;  
  
public class Java01_Object {  
    public static void main(String[] args) {  
        // TODO OOD  
        //todo 1. declare  
        //todo 2. create object  
        //todo 3. declasre attribute  
        // 变量类型 变量名称 = 变量值  
        // 属性类型 属性名称 = 属性值  
  
        // 引用数据类型  
  
        // todo 4: 声明方法  
        Cooking c = new Cooking();  
        c.name = "Beef stew";  
        c.food = "Beef";  
        // todo 5: execute  
        c.execute();  
    }  
    }  
    class Cooking {  
//    特征  
        // 名字  
        String name;  
        String type = "stew";  
        String food;  
        String relish = "soy";  
// ToDo： execute        void execute() {  
            System.out.println("start");  
        }  
    }
```

![[Pasted image 20240418235021.png]]
![[Pasted image 20240418235254.png]]

#### static

 ==// 和类相关的属性成为静态属性==  
==//和类相关的方法 - 静态属性==  
```
package chapter04;  
  
public class Java02_Object {  
    public static void main(String[] args){  
       
        Bird.fly();  
        System.out.println(Bird.type);  
    }  
  
    class Bird {  
        static String type = "bird";  
        static void fly() {  
            System.out.println("flying");  
        }  
    }  
}
```

注意事项：
元空间 （方法区） - 类的信息 User
栈 -（方法，变量）User user
堆 - 对象 User

![[Pasted image 20240419090035.png]]

![[Pasted image 20240419090546.png]]

```
代码块，是在构造对象之前执行的
User11 user = new User11("zhangwen") // 构造对象
user.test();

```
#### inheritance
OOP三个特征：继承，封装，多态
类存在父子关系，子类可以直接获取父类的成员属性和方法
单继承，一个父类可以多子类，但一个子类只有一个父类
```
package chapter04;  
  
public class Java04_inheritance {  
    public static void main(String[] args) {  
        // TODO 面向对象 - 继承 extends        Child c = new Child();  
        System.out.println(c.name);  
        c.test();  
    }  
}  
  
class Parent {  
    String name = "zhangwen";  
  
    void test() {  
        System.out.println("test");  
    }  
}  
  
class Child extends Parent {  
  
}
```

// 构造方法 
```
package chapter04;  
  
public class Java04_inheritance {  
    public static void main(String[] args) {  
        // TODO 面向对象 - 继承 extends        
	    // 构造方法
	    // 父类对象是在子类对象创建前创建完成，创建子类对象前，会调用父类的构造方法完成父类的创建
        Child c1 = new Child();  
        Child c2 = new Child();  
        Child c3 = new Child();  

    }  
}  
  
class Parent {  
    String name = "zhangwen";  
	Parent() {
		System.out.println("parent");  
	} 
}  
  
class Child extends Parent {  
  Child() {
		System.out.println("child");  
	}
}

// 返回三个parent和三个child
```


// 默认情况下，子类对象构建时候，会默认调用父类的构造方法，使用的super的方式，
如果父类提供构造方法，那么JVM不会提供默认的构造方法，子类应该显示调用super来创建父类对象
```
class Parent {  
    String username;
	Parent(String name) {
		username = name;
		System.out.println("parent");  
	} 
}  
  
class Child extends Parent {  
  Child() {
	  super("zhangwen");
	  System.out.println("child");  
	}
}
```

#### 多态
一个对象在不同场景下表现出来的不同的状态

一个对象的可以使用的功能取决引用变量的类型。

```

public static void main(String[] args){
	Person p = new Person();
	Person p1 = new Boy();
	p1.testPerson();
	// p1.testBoy(); //这样是不对的，多态语法实际是对对象的使用场景进行了约束。

	Person p2 = new Girl();
	Boy boy = new Boy();
	boy.testBoy(); // 这样是可以的
}
class Person {
	void testPerson(){
	  System.out.println("person");  
	}
}
class Boy extends Person {
	void testBoy(){
		  System.out.println("boy");  
		}

}

class Girl extends Person {
	void testGirl(){
	  System.out.println("girl");  
	}
}
```

#### 方法重载

// 一个类中，不能重复声明相同的方法，也不能声明相同的属性
// 相同的方法指的是 方法名参数列表相同，和返回值类型无关。
// 如果方法名字，相同，但是参数列表（个数，顺序，类型）不同，是不同的方法。


%% 构造方法也可以重载 %%
```
public static void main(String[] args){
	
}
class User14 {
 // 构造方法的重载
 User14() {
 
 }
  User14(String namne) {
 
 }
	void login(String name, String password){
	  System.out.println("账号，密码登录");  
	}
	void login(int tel){
	  System.out.println("手机登录");  
	}
}
```
#### 方法重写
![[Pasted image 20240420005635.png]]
![[Pasted image 20240420005728.png]]
![[Pasted image 20240420010043.png]]

#### 访问权限

Java只能有一个公共类，而且必须和文件名相同
main方法： 公共的，因为JVM可以任意调用，不用考虑权限问题

private: 私有，同一个类可以使用
default: 默当不设定任何权限的时候，JVM会提供包权限。
protected: 子类可以访问。
public： 公共的
```
public static void main(String[] args){
	User18 user = new User18();
	sout(user.name) // 这样不行
	sout(user.username) // 这样不行
}

class User18 {
private String name;
public String username;
	void test() {
	sout(name);
	}
}
```

#### 内部类：
```
// java 不允许外部类使用private对象

// 内部类，就是类中声明的类

// 因为内部类可以看作外部类的属性，需要构建外部类对象才可以使用。

public class Java_object {
	public static void main(String[] args){
		OuterClass outer = new OuterClass();
		OuterClass.InnerClass innerClass = outer.new InnerClass();
	}
}

class OuterClass {
	public class innerClass{
	}
}


```

#### final

// java 提供了一种语法，可以在数据初始化后不被修改，final可以修饰变量，变量的值一旦初始化
无法修改
// 一般final修饰的变量称之为常量
// final 可以修饰属性，那么JVM无法自动进行初始化，需要自己进行初始化，属性值不能发生变化
// final可以修饰方法，这个方法不能赋予子类重写
// final 不能修饰构造方法
==// final 可以修饰类，这样就不能有子类==
// 可以修饰方法的参数，一旦修饰，无法修改
```
public class Java_object {

	public static void main(String[] args){
		String name = "zhangsan";
		User20 user = new User20("wang");
			// 不行
			user.name = "zhangsan";
			System.out.println(user.name); // zhangsan
			
			user.name = "zhangli";
			System.out.println(user.name); // zhangli
		
	}
}

（如果加了final）class User20 {
	public final String name;
	
	public User20(String name) { //构造方法
		this.name = name;
	}
	public final void test() {
	
	}
}

// 加了final 这一段就不行。
class Child20 extends User20 {
	public void test() { // 不行
	}
}
```

#### abstract 抽象

抽象 - abstract
抽象类: 不完整的类，就是抽象类
抽象方法 - 只有声明，没有实现的方法。
抽象类无法构建对象。

分析问题：对象 => 类，从具体到抽象。
写代码：先声明类，再创建对象。从抽象到具体。

// 如果一个类含有抽象方法，那么这个类是抽象类
// 如果一个类是抽象类，它方法不一定是抽象方法

// 抽象类无法构建对象，但是可以通过子类简介构建对象。
==final 不能和abstract 一起使用。==

```
public class Java_object {
	public static void main(String[] args){
		Chinese21 c = new Chinese21();
		
		
	}
}
abstract class Person {
	public abstract void eat(); // 如果抽象类含有抽象方法，子类继承，需要重写抽象方法，补充完整
	public void test() {
		
	}
}

class Chinese21 extends Person {
	public void eat() {
	}
}
```

#### interface 接口

接口，可以理解为规则
基本语法:
interface 接口名称 { 规则属性， 规则的行为 }
接口是抽象的。
规则的属性必须是固定值，并且不能修改
属性和行为的访问权限必须为公共的
属性应该是静态的。意思是跟对象的无关，是跟类相关的。
行为是抽象的
接口和类是两个层面的东西
类的对象需要遵循接口，意思是 实现，类需要实现接口，而且可以实现多个接口。

```
public class Java_object {
	public static void main(String[] args){
		// 面向对象 - interface
		
		Computer c = new Computer();
		Light light = new light();
		c.useb1 = light;
		c.powerSupply();
		Light light2 = new light();
		c.useb2 = light2;
		c.powerSupply();
	}
}

interface USBInterface {

}

interface USBSupply extends USBInterface{
	public void powerSupply(); //抽象，因为每个实现是不一样的。
}

interface USBReceive extends USBInterface{
	public void powerReceive();
}

class Computer implements USBSupply {
		public USBReceive usb1;
		public USBReceive usb2;
		
		public void powerSupply() {
			usb1.powerReceive();
			usb2.powerReceive();
		}
		public void powerReceive() {
		}
}

class Light implements USBSupply {
		
		public void powerReceive() {
			
		}

}
```

## 安全实践
![[Pasted image 20240616225811.png]]
#### 威胁建模
![[Pasted image 20240616233534.png]]
![[Pasted image 20240616233738.png]]
![[Pasted image 20240616233714.png]]
![[Pasted image 20240616233852.png]]
![[Pasted image 20240616233917.png]]
![[Pasted image 20240616234002.png]]
![[Pasted image 20240616234054.png]]
![[Pasted image 20240616235535.png]]
####  clean code
![[Pasted image 20240617022723.png]]
![[Pasted image 20240617022752.png]]![[Pasted image 20240617022823.png]]![[Pasted image 20240617022842.png]]![[Pasted image 20240617022850.png]]![[Pasted image 20240617022902.png]]![[Pasted image 20240617022909.png]]![[Pasted image 20240617022926.png]]![[Pasted image 20240617022934.png]]![[Pasted image 20240617022959.png]]![[Pasted image 20240617023006.png]]![[Pasted image 20240617023018.png]]


![[Pasted image 20240617015557.png]]

![[Pasted image 20240617015724.png]]

#### 软件重构 refactoring
在不改变代码外在行为，对代码做出修改，改进程序的内部结构
![[Pasted image 20240617020740.png]]
![[Pasted image 20240617021645.png]]
![[Pasted image 20240617022421.png]]


## 测试

#### 单元测试
![[Pasted image 20240617012519.png]]
![[Pasted image 20240617012703.png]]
#### 怎么做unit test
![[Pasted image 20240617012755.png]]
![[Pasted image 20240617012813.png]]
![[Pasted image 20240617013039.png]]
![[Pasted image 20240617013101.png]]
![[Pasted image 20240617113020.png]]
![[Pasted image 20240617113028.png]]
![[Pasted image 20240617113123.png]]

##### 异常测试
![[Pasted image 20240617113211.png]]
![[Pasted image 20240617113244.png]]
![[Pasted image 20240617113949.png]]![[Pasted image 20240617114003.png]]
![[Pasted image 20240617114018.png]]
![[Pasted image 20240617114041.png]]

### unit test principle - first
fast - 
![[Pasted image 20240617111552.png]]
isolated 
![[Pasted image 20240617111610.png]]
repeatable 
self-validating - 必须通过assert运行结果，而不是人工
timely 及时
![[Pasted image 20240617111746.png]]
## 程序员的一天
1、需求串讲
2、需求分析
	文档- task： 例如登录，1. unit test 2. page UI 3. Interface 4.前后端的重构
3、软件设计
	分解问题-模式识别-抽象化-算法
4、代码提交
![[Pasted image 20240418012536.png]]
5、CI/CD
6、代码检视
show case - design - code review
7、软件重构和维护
![[Pasted image 20240418013422.png]]
![[Pasted image 20240418013428.png]]


![[Pasted image 20240501214927.png]]
![[Pasted image 20240501215420.png]]![[Pasted image 20240501215530.png]]


## 代码编程规范
![[Pasted image 20240501223710.png]]

![[Pasted image 20240501224555.png]]

![[Pasted image 20240501224641.png]]

![[Pasted image 20240501225028.png]]
![[Pasted image 20240501225039.png]]
![[Pasted image 20240501225049.png]]
![[Pasted image 20240501225132.png]]
![[Pasted image 20240501225151.png]]

## Java编程实践
![[Pasted image 20240501225300.png]]
![[Pasted image 20240501225454.png]]

![[Pasted image 20240501225823.png]]
![[Pasted image 20240501225842.png]]
![[Pasted image 20240501225945.png]]
![[Pasted image 20240501230047.png]]
![[Pasted image 20240501230059.png]]
![[Pasted image 20240501230149.png]]
![[Pasted image 20240501230216.png]]

![[Pasted image 20240501230245.png]]
![[Pasted image 20240501230259.png]]
![[Pasted image 20240501230348.png]]

### 编程实践
![[Pasted image 20240501230512.png]]
![[Pasted image 20240501230553.png]]
![[Pasted image 20240501231917.png]]

![[Pasted image 20240501232028.png]]
![[Pasted image 20240501232141.png]]
![[Pasted image 20240501232219.png]]

#### 类、接口与面向对象
![[Pasted image 20240501233027.png]]
![[Pasted image 20240501233042.png]]

![[Pasted image 20240501233219.png]]
![[Pasted image 20240501233245.png]]
### 异常处理
![[Pasted image 20240501233521.png]]
![[Pasted image 20240501233605.png]]

### 敏感异常

![[Pasted image 20240617142247.png]]
![[Pasted image 20240617142607.png]]

![[Pasted image 20240617142020.png]]
![[Pasted image 20240617142105.png]]

### 并发与多线程
