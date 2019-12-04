# 原创：MFC 部分概念【持续补充】

**                                                             目    录**

[问：设备描述表DC是一个什么概念，谁通俗的说说，先谢了](#%E9%97%AE%EF%BC%9A%E8%AE%BE%E5%A4%87%E6%8F%8F%E8%BF%B0%E8%A1%A8DC%E6%98%AF%E4%B8%80%E4%B8%AA%E4%BB%80%E4%B9%88%E6%A6%82%E5%BF%B5%EF%BC%8C%E8%B0%81%E9%80%9A%E4%BF%97%E7%9A%84%E8%AF%B4%E8%AF%B4%EF%BC%8C%E5%85%88%E8%B0%A2%E4%BA%86)

[问：DC，CDC，HDC，CClientDC....有什么本质的区别？](#%E9%97%AE%EF%BC%9ADC%EF%BC%8CCDC%EF%BC%8CHDC%EF%BC%8CCClientDC....%E6%9C%89%E4%BB%80%E4%B9%88%E6%9C%AC%E8%B4%A8%E7%9A%84%E5%8C%BA%E5%88%AB%EF%BC%9F)

[CWnd：](#CWnd%EF%BC%9A)

[CDocument：](#CDocument%EF%BC%9A)

[CView：](#CView%EF%BC%9A)

[CDC：](#CDC%EF%BC%9A)

[CDialog：](#CDialog%EF%BC%9A)

[CWinApp：](#CWinApp%EF%BC%9A)

[CGdiObject及子类，](#CGdiObject%E5%8F%8A%E5%AD%90%E7%B1%BB%EF%BC%8C)

[问：解释一下VC中的CDC *pDC=pWnd-&gt;GetDC(); ](#%E9%97%AE%EF%BC%9A%E8%A7%A3%E9%87%8A%E4%B8%80%E4%B8%8BVC%E4%B8%AD%E7%9A%84CDC%C2%A0*pDC%3DpWnd-%3EGetDC()%3B%C2%A0)

[问：VC++中绘图用到的this-&gt;GetDC()函数是什么作用？还有 this-&gt;ReleaseDC(pDC)](#%E9%97%AE%EF%BC%9AVC%2B%2B%E4%B8%AD%E7%BB%98%E5%9B%BE%E7%94%A8%E5%88%B0%E7%9A%84this-%3EGetDC()%E5%87%BD%E6%95%B0%E6%98%AF%E4%BB%80%E4%B9%88%E4%BD%9C%E7%94%A8%EF%BC%9F%E8%BF%98%E6%9C%89%C2%A0this-%3EReleaseDC(pDC))

---


DC(Device Context)，设备上下文或者设备环境。<br/>
不同设备的上下文含义是不一样的，虽然都是叫DC，但不同设备的DC，其作用是不同的。 <br/>
 

### 问：设备描述表DC是一个什么概念，谁通俗的说说，先谢了

<br/>
学习VC，首先遇到的就是这个DC,即设置描述表，输出文字，绘图都要用这个，好象它太重要了。但是我就是不明白，这是什么东西。 一些教程看了，但还是不太了解，谁能通俗的说说，能快速理解它，谢谢。 <br/>
答：<br/>
1、作画之前需要准备好画布、画笔、调色板等。当使用GDI函数如MoveToEx/LineTo, TextOut时，只是告诉系统要划线或写字了，但用什么样的笔（HPEN），字是什么颜色(SetTextColor)，画在哪张“纸”(HBITMAP)上,需要从一个由系统定义的数据结构中去读取,这个数据结构被称为Device Context(DC)。 换句话说，GDI函数只是绘画的动作，而DC则保存了绘画所需的材料和工具。 <br/>
2、设备环境函数（Device Context） 设备环境是一个结构，它定义了一系列图形对象及其相关的属性，以及会影响输出结果的绘图方式。这些图形对象包括：画笔（用于画直线），笔刷（用于绘图和填充），位图（用于屏幕的拷贝或滚动），调色板（用于定义可用的颜色集），剪裁区（用于剪裁和其他操作），路径（用于绘图和画图操作）。设备环境函数用于对设备环境进行创建、删除或获取信息。

### <br/>
问：DC，CDC，HDC，CClientDC....有什么本质的区别？

<br/>
答：<br/>
都是DC嘛，HDC就是最原始的 DC 句柄，很多API的第一个参数就是一个HDC类型，比如<br/>
HDC hDC = ::GetDC( m_hWnd);<br/>
::MoveToEx( hDC, 0, 0, NULL );<br/>
::LineTo( hDC, 0, 100, );<br/>
::ReleaseDC( m_hWnd, hDC );<br/>
在MFC中，为了将API封装成一个类来操作，因此多出来了一个CDC。所以在MFC中，都是<br/>
CDC dc = GetDC();<br/>
dc.MoveTo( 0, 0 );<br/>
dc.LineTo( 0, 100 );<br/>
this-&gt;ReleaseDC( &amp;dc );<br/>
但这样还不够，因为 CDC还要你自己去释放，所有MFC中又多出来一个CClientDC，这样你就可以这样了： <br/>
CClientDC dc(this);<br/>
dc.MoveTo( 0, 0 );<br/>
dc.LineTo( 0, 100 );<br/>
CClientDC的析构函数自己会释放自己(见下文)。<br/>
DC不是什么对象，就是设备上下文的简称。 与CClientDC一样，还有CWindowDC，CPaintDC，只是它们的绘制范围不一样。<br/>
但弄到底，都只是HDC的一些封装而已，你可以在CDC类中直接引用m_hDC，这就是那个原始的HDC句柄了。<br/><br/>
CDC是MFC的DC的一个类。<br/>
HDC是DC的句柄，API中的一个类似指针的数据类型。<br/>
MFC类的前缀都是C开头的，H开头的大多数是句柄。<br/>
这是为了助记，是编程读\写代码的好的习惯。<br/>
CDC是所有MFC的DC类的基类。常用的CClientDC dc(this);就是CDC的子类(或称派生类)。<br/>
CDC等设备上下文类(DC类)，都含有一个类的成员变量m_nHdc，即HDC类型的句柄。<br/>
记住下面的一句话，会有助于你的理解：<br/>
MFC的类，是在用window API语句开发出来的有一定功能的小程序。使用它的默认方法就是记住它的名字与参数(可以用笔记，代替脑记)。 

### <br/><br/>
CWnd：

窗口类，它是大多数“看得见的东西”的父类（Windows里几乎所有看得见的东西都是一个窗口，大窗口里有许多小窗口），比如视图CView、框架窗口CFrameWnd、工具条CToolBar、对话框CDialog、按钮CButton，etc；一个例外是菜单（CMenu）不是从窗口派生的。该类很大，一开始也不必学，知道就行了。

 

### CDocument：

文档类，负责内存数据与磁盘的交互。最重要的是OnOpenDocument(读入),OnSaveDocument（写盘）,Serialize（读写）

 

### CView：

视图类，负责内存数据与用户的交互。包括数据的显示、用户操作的响应（如菜单的选取、鼠标的响应）。最重要的是OnDraw(重画窗口)，通常用CWnd::Invalidate()来启动它。另外，它通过消息映射表处理菜单、工具条、快捷键和其他用户消息。你自己的许多功能都要加在里面，你打交道最多的就是它。

 

### CDC：

设备上下文/设备环境类。无论是显示器还是打印机，都是画图给用户看。这图就抽象为CDC。CDC与其他GDI（图形设备接口）一起，完成文字和图形、图像的显示工作。把CDC想象成一张纸，每个窗口都有一个CDC相联系，负责画窗口。CDC有个常用子类CClientDC（窗口客户区），画图通常通过CClientDC完成。

### <br/>
CDialog：

对话框类

### <br/>
CWinApp：

应用程序类。似于C中的main函数，是程序执行的入口和管理者，负责程序建立、消灭，主窗口和文档模板的建立。最常用函数InitInstance（）：初始化。

### <br/>
CGdiObject及子类，

用于向设备文本画图。它们都需要在使用前选进DC。 CPen笔，画线 CBrush刷子，填充 CFont字体，控制文字输出的字体 CBitmap位图 CPalette调色板 CRgn区域，指定一块区域可以用于做特殊处理。

CFile：文件类。最重要的不外是Open（打开）,Read（读入）,Write（写）

CString字符串。封装了C中的字符数组，非常实用。

CPoint：点类，就是（x, y）对<br/>
CRect：矩形类，就是（left, top, right, bottom）<br/>
CSize：大小类，就是（cx, cy）对（宽、高）<br/><br/>
Windows引入了与具体设备无关的图形设备环境(DC) 进行显示。MFC定义了设备环境类----CDC。<br/>
CDC与CGdiObject的关系<br/>
说到CDC类就不能不提一下CGdiObject---图形对象类。 在Windows应用程序中，设备环境与图形对象共同工作，协同完成绘图显示工作。就像画家绘画一样，设备环境好比是画家的画布，图形对象好比是画家的画笔。用画笔在画布上绘画，不同的画笔将画出不同的画来。选择合适的图形对象和绘图对象，才能按照要求完成绘图任务。<br/>
有关CDC类的继承<br/>
父类：从 CObject 直接继承而来。继承了CObject类的各种特性，如动态创建等等。<br/>
子类：<br/>
CClientDC-------代表操作窗口的DC ，是比较常用的一个子类.<br/>
CMetaFileDC ------响应Meta File的DC ，Meta File是一些GDI消息。<br/>
CPaintDC-------响应WM_PAINT消息的DC。<br/>
CWindowDC ------代表整个屏幕的DC。<br/>
CDC类的数据成员<br/>
数据成员只有两个：<br/>
HDC m_hDC : CDC对象使用的输出设备上下文。<br/>
HDC m_hAttribDC : CDC对象使用的属性设备上下文。<br/>
二者在CDC对象创建时指向相同的设备上下文。

### <br/><br/>
问：解释一下VC中的CDC *pDC=pWnd-&gt;GetDC(); 

<br/>
答：绘图用到的所有有关的类与函数都被集合到一起，被称之为设备上下文，或设备环境。你可以将这个类集看成一个超级的大类。GetDC()是一个函数，它能获得DC的使用权，也就是说它将句柄（或指针）交给了你，也就是说它将使用它的钥匙交给了你。你可以使用它的所有函数了。不用再向API函数那样，每一个绘图动作都要使用一个函数，如果你不想改变它的默认值，可以直接绘图，当然，他提供了比API更加强大的函数与更加多的功能。当然，对初学者，最方便的是，不用记大量的函数了，当你用它实例化一个对象后（也称得到设备上下文（DC）），你只要用“-&gt;”或“.”运算符就可以在VC提示的帮助下来选择相应的函数了。<br/>
CDC *pDC=pWnd-&gt;GetDC();<br/>
1.用CDC（MFC的设备上下文）实例化一个对象的指针<br/>
2.为这个对象的指针赋值为pWnd<br/>
3.pWnd被赋值为GetDC。相当于用API的DC实例化一个对象的指针pWnd<br/>
小结：用MFC的设备上下文实列化一个指针的对象，这个指针对象的值来源于API的设备上下文实例化。<br/>
＝＝＝＝＝＝＝＝＝＝＝＝＝＝<br/>
实际上，MFC的大多数调用的函数，最终调用的都是API里的相应的函数

### <br/>
问：VC++中绘图用到的this-&gt;GetDC()函数是什么作用？还有 this-&gt;ReleaseDC(pDC)

<br/>
答：<br/>
1、this指针是当前类的对象的指针，它指向类实例化后的对象。它是隐含的指针，每个对象都有一个。<br/>
2、this-&gt;GetDC();得到DC，相当于<br/>
CDC *pDC;<br/>
pDC-&gt;GetDC();<br/>
也相当于<br/>
CDC dc;<br/>
dc.GetDC();<br/>
3、this-&gt;ReleaseDC();是释放DC<br/><br/>
CClientDC类<br/>
CClientDC派生于CDC，在构造时调用了Windows函数GetDC，在析构时调用了ReleaseDC。这意味着和CClientDC对象相关的设备上下文是窗口的客户区。<br/>
几种DC及区别<br/>
CClientDC：（客户区设备上下文）用于客户区的输出，与特定窗口关联，可以让开发者访问目标窗口中客户区，其构造函数中包含了GetDC，析构函数中包含了ReleaseDC。用法是：<br/>
CClientDC dc(this);//this一般指向本窗口或当前活动视图<br/>
dc.TextOut(10,10,str,str.GetLength());//利用dc输出文本，如果是在CScrollView中使用，还要注意调用OnPrepareDC(&amp;dc)调整设备上下文的坐标。<br/>
CPaintDC：用于响应窗口重绘消息（WM_PAINT）时的绘图输出。CPaintDC在构造函数中调用BeginPaint()取得设备上下文，在析构函数中调用EndPaint()释放设备上下文。EndPaint()除了释放设备上下文外，还负责从消息队列中清除WM_PAINT消息。因此，在处理窗口重画时，必须使用CPaintDC，否则WM_PAINT消息无法从消息队列中清除，将引起不断的窗口重画。CPaintDC也只能用在WM_PAINT消息处理之中。<br/>
CWindowDC：关联一特定窗口，允许开发者在目标窗口的任何一部分进行绘图，包含边界与标题，这种DC同WM_NCPAINT消息一起发送。<br/>
CWindowDC与CClientDC，CPaintDC的区别：CWindowDC可在非客户区绘制图形，而CClientDC，CPaintDC只能在客户区绘制图形。CWindowDC下坐标原点是在屏幕的左上角，CClientDC，CPaintDC下坐标原点是在客户区的左上角。<br/>
CClientDC与CPaintDC的区别：CPaintDC的对象一般用在OnPaint内以响应Windows消息WM_PAINT，自动完成绘制，在整个窗口内进行重画，维持原有窗口完整性。CClientDC应用在非响应Windows消息WM_PAINT的情况下，进行实时绘制，绘制的区域内被重画。<br/>
所需头文件：#include &lt;afxwin.h&gt;
