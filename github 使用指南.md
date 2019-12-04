# 原创：github 使用指南

**github的好处：**

多人协作，多分支

> 


github的目的：托管项目代码

github建立在git的环境上。一个git库对应一个

**名词解释：**

> 
（1）repository【仓库】 / Git Project： 存放项目代码，开源项目
（2）star【收藏】 收藏项目，方便查找（100个收藏很不容易）
（3）Fork【复制，克隆】 把张三的项目直接fork过去，一模一样【独立存在】

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMxLnpoaW1nLmNvbS92Mi05NzI3MmI5YTNiNDQ2MTEyYWJhMjA0YWJmYWEzMGU4MF9iLnBuZw?x-oss-process=image/format,png)
> 
（4）pull request 【发起请求，把更新动作发送过去】 单独添加代码。发起请求等待李四查看，并在张三同意后合并到原仓库  
（5）Watch【关注项目】 有任何更新，都可以查看到通知  
（6）Issue【发现bug，及时讨论】  
（7）commit【一瞬间拍下来，截图】  
（8）branch【master主+fearure复制品（需要被合并）】  
（9）topic 给自己的项目设置 topic 后，相当于自己给自己的项目设置了一个 tag ，这样可以方便别人搜索。比如要搜索所有 topic 为 android 的项目，你只需要在 GitHub 搜索时输入 `topic android ` 然后搜索即可。  
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMzLnpoaW1nLmNvbS92Mi0zMTg2OTU0MTU1ODNmZjExMTUzZDZjNTMxYTcxYzgzMl9iLnBuZw?x-oss-process=image/format,png)
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMxLnpoaW1nLmNvbS92Mi1jYzkyNTk3ZTQwZTBhNzhmYWFlOGMzOWQwNGZjNjczY19iLnBuZw?x-oss-process=image/format,png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMyLnpoaW1nLmNvbS92Mi1kODZkYWY3NTM5Mjg4OTZiZTAyZGYxNDMyOGVkYjE0MV9iLnBuZw?x-oss-process=image/format,png)


**快捷键t：findfile**

功能详细：

Issue【发现bug，及时讨论】

开源项目贡献：

> 
（1）新建Issue  
（2）pull Request
———fork  
———修改  
———pull request  
———等待作者操作


---


git：通过git管理github托管项目代码

##  

第一部分：本地仓库
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMxLnpoaW1nLmNvbS84MC92Mi1hYzdkNTNiZTA5ZmM4MzY5ODJjZjZiYWEzZWVkMjlmM19oZC5wbmc?x-oss-process=image/format,png)
> 
git add test.python【放到暂存区】


> 
git status【查看状态】


> 
git commit -m "提交描述"


先初始化用户信息：
!["打错了，下面应该是user,email"](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMxLnpoaW1nLmNvbS84MC92Mi1hN2YwMTIzNGJlMjYxNjM2Mzc5Mzc3MGQ5YmJjZTI5Zl9oZC5wbmc?x-oss-process=image/format,png)



 ![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWM0LnpoaW1nLmNvbS84MC92Mi0xMzZiOWJkMmIxYTk1MmY2Njc1MmUzYjMwM2MzOWZlYl9oZC5wbmc?x-oss-process=image/format,png)

暂存
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMzLnpoaW1nLmNvbS84MC92Mi01NmI5ZTU5MWIyYjliODYzYzdiZDYwNzIzYTEzNzc5OF9oZC5wbmc?x-oss-process=image/format,png)
暂存区已经有了

然后：git add hello.py
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWM0LnpoaW1nLmNvbS84MC92Mi1kY2Q2ZmVhY2QyZDA4YTBiZDNmNmNmMTcwZjExYjNlMl9oZC5wbmc?x-oss-process=image/format,png)

修改文件上传：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWM0LnpoaW1nLmNvbS84MC92Mi04NTFmZTA4YWE1MTYwMTkxMWE0YzAxOTg5MzAyOGE0MV9oZC5wbmc?x-oss-process=image/format,png)

删除文件：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMxLnpoaW1nLmNvbS84MC92Mi0xNTBiNGM0OWU2MWVjZjJlODkyYjMyMjRhMDk1ODk4N19oZC5wbmc?x-oss-process=image/format,png)

删除

##  

第二部分：远程仓库
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMyLnpoaW1nLmNvbS84MC92Mi1mYmM5YTk1N2EyYTZmYWRkNDdhYWZlYzk3ZjAyMGM1OV9oZC5wbmc?x-oss-process=image/format,png)

> 
（1）先克隆

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWM0LnpoaW1nLmNvbS84MC92Mi1hMmE4MzI2ZWVmZjQwZjY1ZGE1OGY0YjlkZmEwMTBjOF9oZC5wbmc?x-oss-process=image/format,png)
> 
git clone 仓库地址


一次输入账户信息就足够了

（2）然后按之前的操作顺序存放到本地仓库


- git add ...



- git commit ... -m "..."



- git push


（3）git push
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMyLnpoaW1nLmNvbS84MC92Mi01MDlhMjIwMTNjZDk0ZDY0MjFmZTA3MGI2ZTA2NDA2M19oZC5wbmc?x-oss-process=image/format,png)
修改权限：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9waWMzLnpoaW1nLmNvbS84MC92Mi0yOTcxMDNmYzAyOGVmOGY2NjJjZjA0ZGUxYjVhNzgxNl9oZC5wbmc?x-oss-process=image/format,png)
在github页面查看成功：

 

 

##  

使用建议

> 
●对于一些可能会经常发生变化的会不定期更新的好项目 多使用 watch. 比如 android-cn 团队的 [android-discuss](https://link.jianshu.com/?t=https%3A%2F%2Fgithub.com%2Fandroid-cn%2Fandroid-discuss) 项目，你就可以 watching 它，这里面都是一些关于 Android 技术的交流，如果有任何新问题，你都可以收到通知，你可以查看别人的回答，你也可以回答别人提出的问题，这是一个很好的学习成长方式。  
●只要项目新增一些好玩好用的东西，你就会收到通知。  
●知乎上有这样的问题： github 上有哪些值得 watch 的项目  
●值得注意的是，如果 watch多了，你可能会被无休止的邮件通知烦死（邮件通知可设置），因为被 watch 项目有任何留言、PR等更新都会触发通知，所以做好权衡。  
●喜欢一个项目就 star 它吧~  
●修改开源项目就使用 fork，这样你就可以在原项目的基础上，对项目进行修改提交，现在你是这个项目的主人啦~  


 

参考：

[https://www.bilibili.com/video/av39189147](https://www.bilibili.com/video/av39189147)

[https://www.cnblogs.com/bibi-feiniaoyuan/p/9519467.html](https://www.cnblogs.com/bibi-feiniaoyuan/p/9519467.html)

[https://www.bilibili.com/video/av39189147](https://www.bilibili.com/video/av39189147?)

如何正确设置邮箱【先放着，以后看】：[如何正确接收 GitHub 的消息邮件](https://github.com/cssmagic/blog/issues/49)
