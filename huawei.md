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
```
package chapter04;  
  
public class Java02_Object {  
    public static void main(String[] args){  
        // 和类相关的属性成为静态属性  
        //和类相关的方法 - 静态属性  
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
```
public class Java_object {
	public static void main(String[] args){
		// 面向对象 - interface
		
		
	}
}

```

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
