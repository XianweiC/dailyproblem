# MFC一些内置类

VC++具有强大的绘图功能，虽然基于对话框的应用我推荐大家使用C#  Winform程序，但是计算机图形和图像的基础知识，还是强烈推荐使用VC++ MFC实现。这有助于让你深入的理解图形变换、图像处理等知识。     在Windows平台下，GDI（Graphics Device Interface）图形设备接口被抽象为上下文CDC类（Device  Context，DC）。Windows平台直接接收图形数据信息的不是显示器和打印机等硬件设备，而是CDC对象。MFC中，CDC类定义设备上下文对象的基类，封装了所需的成员函数，调用CDC类的成员函数，绘制和打印图形及文字。

​    CDC类派生出CClientDC类、CMetaFileDC类、CPaintDC类和CWindowDC类，请读者自行学习，同时推荐阅读原书。
​     MFC常用CPoint、CRect、CSize等数据类型。
​     (1) CPoint类：存放点坐标(x，y)；
​     (2) CRect类：存放矩形左上顶点和右下角顶点的坐标(top、left、right、bottom)，其中(top，left)为矩形的左上角点，(right，bottom)为矩形的右下角点；
​     (3) CSzie类：存放矩形的宽度和高度的坐标(cx，cy)，其中cx为矩形的宽度，cy为矩形的高度。