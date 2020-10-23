# angular学习
-----------------

## 传统js开发特点

- 基于事件驱动
- 手工dom操作
***
## angular开发特点

### **typescript取代javascript**

1. 传统js开发没有模块概念，或者使用JavaScript模块加载器比如Require.js。在angular中所有开发都是基于模块的。angular引用第三方包也是基于模块的。
2. typescript变量类型，配合ide进行类型推断。
3. typescript装饰器。

### **数据驱动**

1. angular通过脏值检查，检查值是否发生变化。自动更新视图。
2. 无需手动进行dom操作。
3. 双向绑定，表单验证。

### **rxjs消息订阅**

1. 取代原有ajax功能。
2. 组件与组件通信。

### **开发模式**

1. 组件化开发。
2. 依赖注入。
3. 路由导航。
4. typescript模块与NgModule

## angular基础知识点
<br>
<br>

### *基本概念*

1. 模块

    Angular 自己定义了一套模块系统 NgModule，它和 JavaScript（ES2015） 的模块不同而且有一定的互补性。 NgModule 为一个组件集声明了编译的上下文环境，它专注于某个应用领域、某个工作流或一组紧密相关的能力。 NgModule 可以将其组件和一组相关代码（如服务）关联起来，形成功能单元。

    ngModule实际就是一组组件、服务、管道、接口、类的合集，用于实现某一类的功能，一定要吧ngModule和es6的模块概念区分开。在angular中这是两套概念。

    像 JavaScript 模块一样，NgModule 也可以从其它 NgModule 中导入功能，并允许导出它们自己的功能供其它 NgModule 使用。 比如，要在你的应用中使用路由器（Router）服务，就要导入 Router 这个 NgModule。
2. 组件

    每个 Angular 应用都至少有一个组件，也就是根组件，它会把组件树和页面中的 DOM 连接起来。 每个组件都会定义一个类，其中包含应用的数据和逻辑，并与一个 HTML 模板相关联，该模板定义了一个供目标环境下显示的视图。

    组件其实就是类加上了@Component() 装饰器，组件往往负责页面中的一块区域。是实现功能的最小单位。

3. 模板、指令和数据绑定

    模板会把 HTML 和 Angular 的标记（markup）组合起来，这些标记可以在 HTML 元素显示出来之前修改它们。 模板中的指令会提供程序逻辑，而绑定标记会把你应用中的数据和 DOM 连接在一起。 有两种类型的数据绑定：

    - 事件绑定让你的应用可以通过更新应用的数据来响应目标环境下的用户输入
    - 属性绑定让你将从应用数据中计算出来的值插入到 HTML 中。

4. 服务与依赖注入

    对于与特定视图无关并希望跨组件共享的数据或逻辑，可以创建服务类。 服务类的定义通常紧跟在 “@Injectable()” 装饰器之后。该装饰器提供的元数据可以让你的服务作为依赖被注入到客户组件中。

    服务两个主要作用：
        1、更纯粹的数据处理，不像组件需要模板数据展示、需要处理事件等。
        2、服务可以跨组件通信。

5. 路由

    angular是用于开发单页面的应用的。路由是复杂页面实现视图切换的方式。

    路由器会根据你应用中的导航规则和数据状态来拦截 URL。 当用户点击按钮、选择下拉框或收到其它任何来源的输入时，你可以导航到一个新视图。 路由器会在浏览器的历史日志中记录这个动作，所以前进和后退按钮也能正常工作。

    当用户执行一个动作时（比如点击链接），本应该在浏览器中加载一个新页面，但是路由器拦截了浏览器的这个行为，并显示或隐藏一个视图层次结构。

### *环境搭建*

angular拥有自己的一套开发环境，从项目初始化、创建module、组件、路由、运行、测试。
要想在你的本地系统中安装 Angular，需要安装一下工具：
- Node.js
- npm 包管理器
node中自带npm，只需要安装node就可以了。

安装 Angular CLI


你可以使用 Angular CLI 来创建项目，生成应用和库代码，以及执行各种持续开发任务，比如测试、打包和部署。

要使用 npm 命令安装 CLI，请打开终端/控制台窗口，输入如下命令：
npm install -g @angular/cli


创建工作空间和初始应用

1. 运行 CLI 命令 ng new 并提供 my-app 名称作为参数，如下所示：


    ng new my-app


2. ng new 命令会提示你提供要把哪些特性包含在初始应用中。按 Enter 或 Return 键可以接受默认值。


运行应用
Angular CLI 中包含一个服务器，方便你在本地构建和提供应用。

1. 导航到 workspace 文件夹，比如 my-app。
2. 运行下列命令:

    cd my-app


    ng serve --open

如何搭建环境和Angular CLI详细信息见下面的连接

[搭建本地开发环境和工作空间](https://angular.cn/guide/setup-local)

[CLI 概览与命令参考手册](https://angular.cn/guide/setup-local)

### *目录结构*

![](https://s1.ax1x.com/2020/10/14/05w9Z4.md.png)

如何浏览新项目代码。

1. app.component.ts 是项目的根组件，是第一个要看的文件。
2. app.module.ts 是项目的跟module，在这个文件中查看引用了那些module，最重要的是route module，找到根route，然后一层层浏览查找每一个路由对应的组件。

eg：

![](https://s1.ax1x.com/2020/10/14/05wjkd.md.png)

根route中的路由

![050JhR.png](https://s1.ax1x.com/2020/10/14/050JhR.png)

### *模板数据绑定*

![05bsaQ.png](https://s1.ax1x.com/2020/10/14/05bsaQ.png)

除双向绑定外，angular的数据和事件绑定都是单向数据流。数据绑定是从数据源到视图，事件绑定是从视图到数据源的单向绑定。
angular的数据驱动就是框架通过脏值检查监测数据源发生变化，自动更新视图。

### *依赖注入*

- angular如何创建注入服务

@Injectable 装饰器把类标记为可供注入的服务，可以不需要手工创建实例，框架在需要注入的地方由注入器负责创建服务实例。

![0oQMv9.png](https://s1.ax1x.com/2020/10/15/0oQMv9.png)

在服务中 providedIn: 'root' 直接使用根注入器注入。

![0oQhKs.png](https://s1.ax1x.com/2020/10/15/0oQhKs.png)

在NgModule中注入

![0oQbPU.png](https://s1.ax1x.com/2020/10/15/0oQbPU.png)

在component中注入

在某个注入器的范围内，服务是单例的。也就是说，在指定的注入器中最多只有某个服务的最多一个实例。
Angular DI 具有分层注入体系，这意味着下级注入器也可以创建它们自己的服务实例。 Angular 会有规律的创建下级注入器。每当 Angular 创建一个在 @Component() 中指定了 providers 的组件实例时，它也会为该实例创建一个新的子注入器。 类似的，当在运行期间加载一个新的 NgModule 时，Angular 也可以为它创建一个拥有自己的提供者的注入器。

- 如何使用服务

![0ol1zQ.png](https://s1.ax1x.com/2020/10/15/0ol1zQ.png)

只需要在constructor函数参数中声明就可以，angular注入器会自动将以创建的服务实例注入进来。component中可以直接使用这个服务了。

### *rxjs*

观察者（Observer）模式是一个软件设计模式，它有一个对象，称之为主体 Subject，负责维护一个依赖项（称之为观察者 Observer）的列表，并且在状态变化时自动通知它们。 该模式和发布/订阅模式非常相似（但不完全一样）。

RxJS（响应式扩展的 JavaScript 版）是一个使用可观察对象进行响应式编程的库，它让组合异步代码和基于回调的代码变得更简单。参见 RxJS 官方文档。

angular中异步操作大量使用rxjs，主要用在两个方面。
1. http异步请求。
2. 组件component之间通信。

下面是创建和使用subject的一个例子。

![0o1ZpF.png](https://s1.ax1x.com/2020/10/15/0o1ZpF.png)

在服务中创建了一个subject。

![0o1t6H.png](https://s1.ax1x.com/2020/10/15/0o1t6H.png)

component中使用subject，上图两个方法分别是发送数据和接收数据。

#### rxjs需要掌握的知识点

几种subject：
Subject、BehaviorSubject、ReplaySubject、AsyncSubject
知道 cold、hot、单播、多播。

rxjs操作符

[![0o3Kgg.png](https://s1.ax1x.com/2020/10/15/0o3Kgg.png)](https://imgchr.com/i/0o3Kgg)