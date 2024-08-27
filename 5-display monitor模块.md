# display monitor模块

## 基础知识

### QApplication

QApplication管理GUI程序的控制流和主要设置。

对于用Qt写的任何一个GUI应用，不管这个应用有没有窗口或多少个窗口，有且只有一个QApplication对象

功能

##### QApplication::QApplication(int & *argc*,char ** *argv*)

-  使用在argv中包含的argc个命令行参数，初始化窗口系统及应用对象。

- 有一个全局的指针app指向应用对象（QApplication）。并且只能创建一个QApplication对象。

- QApplication对象必须在绘制设备（设备包括窗口、像素映射、位图等）之前创建。

#### int QApplication::exec()

  进入主循环，知道exit()被调用。

### QWidget

QWidget 类是所有窗口类的父类 (控件类是也属于窗口类), 并且 QWidget 类的父类的 QObject, 也就意味着所有的窗口类对象只要指定了父对象, 都可以实现内存资源的自动回收。

### QAbstractTableModel 

QAbstractTableModel 继承自 QAbstractItemModel，主要用于为 QTableView 提供相关接口，我们可以子类化该抽象类并实现相关接口。本文主要讲 QAbstractTableModel 数据展示和编辑相关的接口如何使用。

### QTableView

 表格视图控件QTableView，需要和QStandardItemModel, 配套使用，这套框架是基于MVC设计模式设计的，M(Model)是QStandardItemModel数据模型，不能单独显示出来。V(view)是指QTableView视图，要来显示数据模型，C(controllor)控制在Qt中被弱化，与View合并到一起。

### QStackedLayout

QStackedLayout继承自QLayout。

QStackedLayout类提供了多页面切换的布局，一次只能看到一个界面。

QStackedLayout可用于创建类似于QTabWidget提供的用户界面。

### QPushButton

按钮是 GUI 开发中最常用到的一种控件，作为一款著名的 GUI 开发框架，Qt 提供了很多种按钮，比如 QPushButton（普通按钮）、QRadioButton（单选按钮）、QToolButton（工具栏按钮）等。

QPushButton 是实际开发中最常使用的一种按钮

### QFont

通过QFont可以部分Qt控件的文字的大小、字体、字间距、下划线等属性

### QHBoxLayout

QBoxLayout可以在水平方向或垂直方向上排列控件，由QHBoxLayout、QVBoxLayout所继承。

QHBoxLayout：水平布局，在水平方向上排列控件，即：左右排列。
QVBoxLayout：垂直布局，在垂直方向上排列控件，即：上下排列。

### QLabel

Qt 提供给我们的一种文本控件，它的基础功能是显示一串文本

### Q_OBJECT

只有加入了Q_OBJECT，才能使用QT中的signal和slot机制，而且Q_OBJECT要放在类的最前面