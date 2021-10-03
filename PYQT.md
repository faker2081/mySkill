# PYQT

pyqt5的类别分为几个模块，包括以下：

- QtCore
  包含了核心的非GUI功能。此模块用于处理时间、文件和目录、各种数据类型、流、URL、MIME类型、线程或进程。

- QtGui
  包含类窗口系统集成、事件处理、二维图形、基本成像、字体和文本。

- QtWidgets
  模块包含创造经典桌面风格的用户界面提供了一套UI元素的类。

- QtMultimedia
  包含的类来处理多媒体内容和API来访问相机和收音机的功能。

- QtBluetooth
  模块包含类的扫描设备和连接并与他们互动。描述模块包含了网络编程的类。这些类便于TCP和IP和UDP客户端和服务器的编码，使网络编程更容易和更便携。

- QtNetwork
  包含了网络编程的类，这些工具能让TCP/IP和UDP开发变得更加方便和可靠。

- QtPositioning
  包含了定位的类，可以使用卫星、WiFi甚至文本。

- Enginio
  包含了WebSocket协议的类。

- QtWebSockets
  模块包含实现WebSocket协议类。

- QtWebKit
  包含一个基于Webkit2图书馆Web浏览器实现类。

- QtWebKitWidgets
  包含的类的基础webkit1一用于qtwidgets应用Web浏览器的实现。

- QtXml
  包含与XML文件的类。这个模块为SAX和DOM API提供了实现。

- QtSvg
  模块提供了显示SVG文件内容的类。可伸缩矢量图形（SVG）是一种描述二维图形和图形应用的语言。

- QtSql
  模块提供操作数据库的类。

- QtTest

  包含的功能，使pyqt5应用程序的单元测试。
  
  ## pyqt5 and matplotlib
  
  ### 关键类
  
  在常见的使用中，我们一般使用plt.plot(x,y,‘r.’)或者subplot这类方法隐含的创建了figure，axes这些对象，为了从**面向对象**角度认识学习matplotlib，我们需要了解清楚各个类的关系和各自作用。
  
  ![matplotlib类继承关系](https://matplotlib.org/_images/inheritance-65ce2e47a854f0550975f5a2d9a9335356c2af71.png)
  
  

思考联系我们日常画画的情景：一张纸（canvas，决定了我们绘制图像的地方）、一支笔（render，负责具体图像的渲染）绘制出图像（artist，我们创建的图像元素，大到figure，小到tick这些都是artist，我们作为“artist”画出来的都是artist）。

思考联系我们日常画画的情景：一张纸（canvas，决定了我们绘制图像的地方）、一支笔（render，负责具体图像的渲染）绘制出图像（artist，我们创建的图像元素，大到figure，小到tick这些都是artist，我们作为“artist”画出来的都是artist）。

**官方链接**:https://matplotlib.org/api/artist_api.html#matplotlib.artist.Artist

官方教程一段话说的很清楚

There are three layers to the matplotlib API.

the matplotlib.backend_bases.FigureCanvas is the area onto which the
figure is drawn
the matplotlib.backend_bases.Renderer is the objectwhich knows how to draw on the FigureCanvas and the
matplotlib.artist.Artist is the object that knows how to use a renderer to paint onto the canvas.

其他如Figure、axes这些类
**各个类的详细资料（官方):** https://matplotlib.org/api/api_overview.html





