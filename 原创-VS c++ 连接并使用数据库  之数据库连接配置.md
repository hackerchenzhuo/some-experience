# 原创：VS c++ 连接并使用数据库  之数据库连接配置

 

## 1、建立数据库

打开SQL Server Management Studio，根据我报告中设计数据库中的表及其之间的依赖关系等等。我的数据库名字为HworkDB，表项如下：

## 2、配置数据源

数据库设计建立完成后，它只是单独的几张表，我们并不能在程序中去访问它，因为程序并不知道数据库在哪里。因此，就要在应用程序跟数据库之间建立连接。

配置数据源说通俗了就是为数据库创建一个对外的窗口，应用程序通过这个窗口来访问数据库中的数据。具体配置步骤为：

      1） 打开 控制面板--〉管理工具--〉数据源，在用户DSN面板选择 “添加”

      2） 在数据源驱动程序中选择 “SQL Server” --〉完成，即打开 “创建到SQL Server 的新数据源”

      3） 在“数据源名称”中填入名称，填 TestSQL01，然后选择 服务器，在其中选择要连接到的SQL Server服务器。（如果电脑的SQL Server服务打开的话，就会有自己的主机名。或者选择网络上的某个SQL Server。

      4） 点击 下一步 配置认证信息

5） 配置完后点击 下一步， 选中 “更改默认的数据库为”复选框，在下拉中选择自己刚才建立的要连接的数据库。 （这一步很重要，一般一个Server上会有多个数据库，如果不更改数据源的默认数据库，你 建立的数据源将连接到默认的数据库，这样就会造成程序中执行SQL语句时“对象名无效”的错误，即找不到你指定的数据表等）

     6） 选择完数据库后直接 下一步--〉完成 就完成了数据源的配置。接下来会出现配置数据源的基本信息，可以通过 “测试数据源”来测试数据源是否配置成功。

## 3、 数据库的连接

建立完数据库，又配置好了数据源，接下来就可以在程序中通过数据源来访问数据库了。

        1） 首先要在程序中引入MFC ODBC数据库的定义文件    #include &lt;afxdb.h&gt;

        2） 定义CDataBase数据库对象，     CDatabase m_db;

        3） 利用CDataBase类的OpenEx函数建立和数据库的连接；

          m_db.OpenEx(_T("DSN=TestSQL01;"),CDatabase::noOdbcDialog);

         /*这里的TestSQL01 即为步骤2中建立的数据源，然后根据OpenEx函数格式填入参数，主要是用户名、密码之类，这里没有设置，所以就没有*/

## 4、 数据库操作

在完成了上面的步骤后，就可以使用SQL语句对数据库进行操作了。基本的操作有 查询、添加、修改、删除等。这里主要说一下查询，其他操作都与添加步骤类似。

     1）查询

     查询的基本步骤可以看下面的这段代码：

<img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238477.png" width="11"/>CString sql = _T("SELECT Password FROM UserInfo    WHERE (UserID =   123“)       //要执行的SQL语句<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238489.png" width="11"/><br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238542.png" width="11"/>     CString psd;    //存放查询结果

 

CDatabase m_db;

CRecordset  rs(&amp;m_db);<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238533.png" width="11"/>     TRY<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238546.png" width="11"/>     {<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238547.png" width="11"/>    rs.Open(AFX_DB_USE_DEFAULT_TYPE,sql);      //打开查询记录<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238543.png" width="11"/>     rs.GetFieldValue(_T("Password"),psd);       //得到数据            <br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238535.png" width="11"/>     }<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238956.png" width="11"/>     CATCH(CDBException,ex)<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238539.png" width="11"/>     {<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238553.png" width="11"/>         AfxMessageBox(ex-&gt;m_strError);<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238564.png" width="11"/>         AfxMessageBox(ex-&gt;m_strStateNativeOrigin);<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238557.png" width="11"/>     }<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238569.png" width="11"/>         AND_CATCH(CMemoryException,pEx)<br/>
{<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238591.png" width="11"/>         pEx-&gt;ReportError();<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238590.png" width="11"/>         AfxMessageBox(_T("memory exception"));<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238598.png" width="11"/>     }<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238583.png" width="11"/>     END_CATCH 

              2）插入

                相对于查询，插入、删除、更改操作就简单得多了。<img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238593.png" width="11"/>                                                                CString sql = _T("USE Test01 INSERT UserInfo(UserID,UserName) VALUES(" 123, 'Bob');

<img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238983.png" width="11"/>             try<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238609.png" width="11"/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238611.png" width="11"/>             ...{                <br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238616.png" width="11"/>                 m_db.ExecuteSQL(sql);<br/><img alt="" height="16" src="https://img-blog.csdnimg.cn/20190624160238636.png" width="11"/>             }
