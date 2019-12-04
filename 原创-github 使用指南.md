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


> 
（4）pull request 【发起请求，把更新动作发送过去】 单独添加代码。发起请求等待李四查看，并在张三同意后合并到原仓库
（5）Watch【关注项目】 有任何更新，都可以查看到通知
（6）Issue【发现bug，及时讨论】
（7）commit【一瞬间拍下来，截图】
（8）branch【master主+fearure复制品（需要被合并）】
（9）topic 给自己的项目设置 topic 后，相当于自己给自己的项目设置了一个 tag ，这样可以方便别人搜索。比如要搜索所有 topic 为 android 的项目，你只需要在 GitHub 搜索时输入 `topic android ` 然后搜索即可。


快捷键t：findfile

功能详细：

Issue【发现bug，及时讨论】

开源项目贡献：

> 
（1）新建Issue
（2）pull Request
———fork
———修改
———pull request


> 
———等待作者操作


---


git：通过git管理github托管项目代码

##  

第一部分：本地仓库

> 
git add test.python【放到暂存区】


> 
git status【查看状态】


> 
git commit -m "提交描述"


先初始化用户信息：

打错了，下面应该是user,email

 

暂存

暂存区已经有了

然后：git add hello.py

修改文件上传：

删除文件：

删除

##  

第二部分：远程仓库

> 
（1）先克隆


> 
git clone 仓库地址


一次输入账户信息就足够了

（2）然后按之前的操作顺序存放到本地仓库

> 
git add ...


> 
git commit ... -m "..."


> 
git push


（3）git push

修改权限：

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
