# panel-magic数据
----------------

## 数据结构

AppDataModel(app数据)-CataDataModel(分组数据)-AppDataObjectModel(页面数据)

## indexdb数据存储

public db = new IndexedDBAngular('panelDataDB', this.dbVersion); 对应数据库
objectStore 对应表,在本应用中认为存储单个页面数据

数据库和表都是有版本的,表的版本用来进行前进和后退的操作,数据库的版本暂时还不知道。

dbCollectionsMoveBackMap: Map<string, MoveBackDBInfoModel> 用于在不同页面、不同动态容器之间快速的查询到专属的撤销前进操作并获取到对应的集合数据。

currentMoveBackMapKey$: BehaviorSubject<string> 当前DBCollectionsMap索引的key,记录当前页面的key,是页面保存在indexdb 中的objectStore key
  
MoveBackDBInfoModel:记录单个页面中的前进后退信息,dbCurrentIndex 和 dbKey 在执行添加数据集操作的时候判断dbCurrentIndex当前指引的下标是否低于dbKey,如果是说明执行了后退操作。
  
## 数据流动相关Subject
 
 - PanelExtendService
  launchSaveIndexedDB$ 执行保存到本地数据库DB操作,此subject控制数据保存进本地数据库。
  PanelExtendComponent 组件中通过如下代码订阅该subject,保存数据。
  ![](https://s1.ax1x.com/2020/04/13/GvKu9A.png)
  widgetList$ 当前自由面板内的组件列表内容,PanelExtendService 通过一下代码订阅该subject,将数据写入appDataService.
  ![](https://s1.ax1x.com/2020/04/14/GzDKvq.png)
  
  
# 画板功能解析
  ---------------
  ## 刻度尺滚动条等组件解析
  - 刻度尺组件讲解
  上方和左侧是刻度尺,代码有待研究
  
  - 滚动条组件讲解
  panel-extend.component.html 在下图的代码中获取滚动条style,确定滚动条位置。
  ![](https://s1.ax1x.com/2020/04/14/GxfB8O.png)
  下面是滚动条的数据模型
  ![](https://s1.ax1x.com/2020/04/14/GxhQeA.png)
  应用初始化时可以看见滚动条的长度和位置都是三分之一。
  
  - 组件的初始化位置刻度
  PanelExtendService 通过如下代码订阅,订阅记录屏幕视图的页面位置信息
  ![](https://s1.ax1x.com/2020/04/14/Gx2B8g.png)
  下面是组件的基准长宽
  ![](https://s1.ax1x.com/2020/04/14/GxIVJ0.png)
  panelRectHeight 高度是计算出来的,每次都不一样。
  panelRectWidth 可以认为是固定的就是主屏幕的宽度。
  PanelExtendService 通过一下代码初始化位置
  ![](https://s1.ax1x.com/2020/04/14/GznjzR.png)
  先发布订阅(上面的图中可以看到PanelExtendService订阅了这个subject),记录主屏幕位置。然后根据主屏幕的大小确定计算起始位置,保证顶部导航在最上面。
  acceptScrollXY方法在这里其实就是通过设置y轴滚动保证顶部导航在最上面的。736是panel-magic的设置的初始主屏幕高度(源代码是给手机准备的)我们的应用是大屏,可以依据实际情况修改。1.8的比例系数很奇怪,这里通过1.8变换了y轴的滚动距离,通过滚动距离设置translateY的时候又还原了。这里我计算过没有这个比例系数也不影响,也可能有影响没看懂。
  下图是acceptScrollXY方法计算translateY时按比例还原的代码。
  ![](https://s1.ax1x.com/2020/04/14/GzKn39.png)
  
  - 关于刻度尺的讲解
  上面已经讲了初始滚动条都在1/3的位置,主屏幕的左上角也是x和y轴的0的位置(注意刻度尺的左上角不一定是0的位置,因为主屏幕初始化的位置不一定在左上角)可以看上面的位置初始化,特别是y轴上的距离计算。
  