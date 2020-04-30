## JavaFX的总体架构

![JavaFX overview of JavaFX internal application structure.](http://tutorials.jenkov.com/images/java-javafx/javafx-overview-1.png)

通常，JavaFX 应用程序包含一个或多个与窗口对应的Stage。 每个舞台上都有一个Scene。 每个Scene都可以附加一个控件、布局等的对象图，称为Scene图。 这些概念后面会有更详细的解释。 

### 1. Stage

基本上一个stage对应一个窗口。

### 2. Scene

一个Stage一次只能拥有一个Scene，但是可以切换Scene。就像舞台上可以切换多个场景一样。

> 您可能想知道为什么 JavaFX 应用程序每个阶段会有多个场景。 想象一个电脑游戏。 一个游戏可能有多个“屏幕”显示给用户。 例如，一个初始的菜单屏幕，主游戏屏幕(游戏进行的地方) ，一个游戏结束屏幕和一个高分屏幕。 每个屏幕都可以用不同的场景来表示。 当游戏需要从一个屏幕切换到下一个屏幕时，它只需将相应的场景附加到 JavaFX 应用程序的 Stage 对象。

### 3.Scene Graph

所有的视觉组件(控制，布局等)必须附加到一个场景显示，并且该场景必须附加到一个舞台，使整个场景可见。 附加到一个场景的所有控件、布局等的总对象图称为场景图。

### 4. Nodes



