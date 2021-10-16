### github使用

**第一步：建立git仓库，cd到你的本地项目根目录下，执行git命令**

```text
git init
```

**第二步：将项目的所有文件添加到仓库中**

```c
git add . # 也能单独添加一个文件，把后面的点换成文件名即可
```

**第三步：将add的文件commit到仓库**

```text
git commit -m "注释语句"
```

**第四步：去github上创建自己的Repository，创建后的页面如下图所示：**

![img](https://pic1.zhimg.com/80/v2-a4e249c5e85f6f5ca6c56fc916c150ac_720w.jpg)

点击**Clone or download**按钮，复制弹出的地址**[git@github.com](mailto:git@github.com):\**\*/test.git**，记得要用SSH的地址，尽量不要用HTTPS的地址，如上图所示

**第五步：将本地的仓库关联到github上---把上一步复制的地址放到下面**

```text
git remote add origin git@github.com:***/test.git
```

**第六步：上传github之前，要先pull一下，执行如下命令：**

```text
git pull origin master
```

**第七步，上传代码到github远程仓库**

```text
git push -u origin master
```



### …or create a new repository on the command line



```
echo "# mySkill" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/faker2081/mySkill.git
git push -u origin main
```

### or push an existing repository from the command line



```
git remote add origin https://github.com/faker2081/mySkill.git
git branch -M main
git push -u origin main
```

更新文件到github其实也差不多的步骤

1.输入指令：git add 文件名称或者 git add.

2.输入指令：git commit -m "这是注释内容"

3.这一步从本地仓库或本地分支获取并集成(整合)，输入指令：git pull origin master

4.如果过程中出现‘please enter a commit message…’,首先按下esc退出键然后输入 ：wq即可

5.输入指令：git push -u origin master

https://blog.csdn.net/s_p_j/article/details/79562047

### 使用心得

master：仅仅是自己github的repository的一个分支（Branch），可以自己命名（命名为main、dev...）的都行。

### 以后更新仓库

1. ```text
   git remote add origin https://github.com/[用户名]/[仓库名].git
   ```

2. ```text
   git branch -M [分支名] # 新建分支（可选），如若上传到老分支中就不用该步
   ```

3. ```text
   git add [要更新的文件名（加上后缀）]
   ```

4. ```text
   git commit -m "first commit"
   ```

5. ```text
   git push -u origin [分支名] # 后面的分支指定你要把add的文件上传到哪个分支，其他教程一般为master、main...
   ```



#### 更新理解

- add：添加内容
- commit：提交所添加的内容
- push：整合到仓库（github）

