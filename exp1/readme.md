#  EXP1

### ①Android Studio版本：

![ASversion](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/ASver.png)



###  ②安装Jupyter Notebook

​	1.**pip install jupyter**

​    2.**jupyter notebook**

​		遇到问题:

![problem](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/problem.png)

​		重新安装tornado：

![solve](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/solveProblem.png)

​		成功运行：

![launch1](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/launch1.png)

![launch2](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/launch2.png)

​	

​	3.**修改默认文件加载路径：**

​		生成配置文件：

![config1](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/config1.png)

​		修改配置文件：

![config2](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/config2.png)

​		修改目标位置（删除后缀）：

![delete](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/config_delete.png)

重新运行：

![path](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/PATH.png)

​	初见notebook：

![test1](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/test1.png)

至此，jupyter notebook完成安装，并且修改了默认加载路径。



### ③安装Anaconda

1. 前往[官方下载页面](https://link.zhihu.com/?target=https%3A//docs.anaconda.com/anaconda/install/windows)下载。

2. 完成下载之后，双击下载文件，启动安装程序。

3. 选择“Next”。

4. 勾选“I Agree”并进行下一步。

5. 仅勾选“Just Me”并点击“Next”。

6. 在“Choose Install Location”界面中选择安装Anaconda的目标路径，然后点击“Next”。

7. 验证安装结果。：

   ① “开始 → Anaconda3（64-bit）→ Anaconda Navigator”，若可以成功启动Anaconda Navigator则说明安装成功。

   ![anacoda](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/anaconda.png)

   ② “开始 → Anaconda3（64-bit）→ 右键点击Anaconda Prompt → 以管理员身份运行”，在Anaconda Prompt中输入 ***conda list\*** ，可以查看已经安装的包名和版本号。若结果可以正常显示，则说明安装成功。

   ![condaList](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp1/Screenshot/condaList.png)