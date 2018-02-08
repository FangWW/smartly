---
title: java web 项目从eclipse迁移到intelliJ IDEA

date: 2017-08-15 23:02:57
cover: https://www.jetbrains.com/idea/img/screenshots/idea_overview_5_1.png

---


**1,配置tomcat**
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea1.jpeg)

**2,配置tomcat和项目**
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea2.jpeg)

**3,配置jdk**
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea3.jpeg)

**4,配置web.xml和webRoot**
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea4.jpeg)

**5,配置项目额外的library**
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea5.jpeg)

**6,Facets**
Facets表述了在Module中使用的各种各样的框架、技术和语言。这些Facets让Intellij IDEA知道怎么对待module内容，并保证与相应的框架和语言保持一致。
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea6.jpeg)

**7,artifact**
artifact是一个项目资源的组合体。例如，一个已编译的java类的集合，一个已打包的java应用。

explode 在这里你可以理解为展开，不压缩的意思。也就是war、jar等产出物没压缩前的目录结构。建议在开发的时候使用这种模式，便于修改了文件的效果立刻显现出来。
![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/img/eclipse2idea7.jpeg)

