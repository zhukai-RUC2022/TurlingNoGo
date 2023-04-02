# 程序设计大作业第一阶段报告

撰写人：梅祎航，杜非原



* #### 小组分工

  *梅祎航：负责主体ui设计和逻辑系统以及实验报告撰写*

  *杜非原：负责ui布局的优化和部分逻辑系统以及实验报告撰写*

  *胡宇：负责代码测试*

* #### 代码框架

  ![代码框架图](image/stage_1_0.png)

​		*如上图，widget为初始界面，包括进入游戏和退出游戏，而pan为下棋界面，包括所有的下棋判定逻辑，倒计时，棋盘绘画*
* #### 代码简介

  ###### 下图是pan.cpp的全部函数

  ![](image/stage_1_3.png)

  * *由于是第一阶段，我们的ui由简洁的两个部分组成，进入界面和游戏界面。后期如有必要可以进一步美观化。*

  * *进入界面较为简单，仅由开始游戏和退出游戏按钮和logo组成（qlable实现），不再赘述。*。

  * *我们的重点——棋盘界面，基本由棋盘——操作区域，功能——控制区域，和逻辑——胜负模块构成。*

  * *棋盘区——由棋子，棋盘构成。*

  * *我们的棋子采用了按钮式设计（Qpushbutton），按钮生成使用了暴力的数组（bushi），在轮到黑棋或白棋下子时，点击相应位置使按钮颜色变为黑/白以实现不同颜色下棋。*

  * *我们的棋盘采用了贴图，最开始的时候希望使用（Qpaintevent）在ui上自画棋盘，但是出现了问题——背景图和棋盘图片无法兼得，最后决定删繁就简，搞了一张贴图。但是我们最古老的棋盘仍有保留在ui最底层，这样即使贴图出了问题也不影响下棋捏~*

  * *功能区——倒计时，开始游戏，暂停游戏，投降按钮，重新开始*

  * *倒计时区域：标签（Qlable）+输入倒计时（单位/s）（QlineEdit）+是否启用倒计时（QRadioButton）（计时器逻辑函数）。*

  * *开始游戏——万物之始，关联计时器（计时器开始工作），关联棋盘（黑棋可以下子）之后轮流下子，判断输赢函数启动。*

  * *暂停游戏——计时器暂停，棋盘冻结不可操作，如果暂停了再按就会继续倒计时*

  * *认输——（没啥说的，摁了就输了）。但是和重新开始不同，认输后需要按开始游戏才能来玩一把*

  * *重新开始——清空棋盘，重设倒计时，重新再来一局（清屏重来函数）。*

  * *逻辑区——黑棋先手，时间判定，判断胜负以及自杀判定，清屏重来*

  * *黑棋先手——设定第一个棋子涂黑就行~*

  * *时间判定——（Qtimer），使用（BeginCountdown）进行倒计时，倒计时归零时判定下棋方输*

  * *判断胜负——judge函数，调用dfs函数判断气有无被断。断气者输，自断者自杀。*

  * *清屏重来——输后清屏，重新开始后清屏。*

* #### 遇到的困难

  * *QT的教程多集中于QT4或QT5，对目前QT6的新更新功能讲解较少，笨人为了给程序添加斗地主的bgm翻遍了csdn没有找到QT6里QMediaPlayer的用法，最后找官方文档才解决*
  * *github的用法比较难，笨人差点把仓库的东西全清空了*
  * *加入BGM后可能需要qt插件，在组内运行时需要解决，否则会使游戏无法运行报错*


* #### 还有想汇报的

  * *在助教的点播下，我们完成了用如下的enum来使工程摆脱oi化*

    ![](image/stage_1_2.png)
  
  * *本组添加了斗地主bgm作为了游戏bgm，符合中国人民的审美趋向，反应了本组”实事求是“的作风，为弘扬中国优秀传统文化，打造文化自信献上了本组的绵薄之力,代码如下*
  
    ```cpp
    player = new QMediaPlayer;
    audioOutput = new QAudioOutput;
    player->setAudioOutput(audioOutput);
    connect(player, SIGNAL(positionChanged(qint64)), this, SLOT(positionChanged(qint64)));
    player->setSource(QUrl::fromLocalFile("E:\\Qt_project\\big_project\\demo\\image\\bgm.mp3"));
    audioOutput->setVolume(50);
    player->setLoops(INFINITY);
    player->play();
    ```
  
  
  *为了实现上述功能，我们在.pro文件中添加了`QT       += multimedia`,并且在.h文件中新增了`#include <QMediaPlayer>`和`#include <QAudioOutput>`两个头文件来使用上述函数*
  
  *这段代码主要来自于Qmediaplay的官方文档，如下图，本组添加了`player->setLoops(INFINITY);`以使得bgm循环播放*
  
  ![](image/stage_1_4.png)
  
  * *本组引入国产之光游戏~~op~~《原神》的派蒙作为游戏的logo（下图左上角），体现了本组对国产游戏的支持和喜爱*
  * *贴心给对战者加入了称号系统，让对战者更有成就感*

![](image/stage_1_1.png)

​	



* ### 特别鸣谢

  * *感谢孙亚辉老师，潘俊达助教在c++学习和大学生活上的悉心指导*
  
  * *感谢由梅祎航，杜非原，胡宇组成的team4小组*
  
  * *感谢中国人民大学信息学院的课程安排和教学平台*
  
  * *感谢八冠王柯洁和2-16的战鹰为本游戏提供了丰富多彩的称号系统*
  
  * *感谢派蒙充当本游戏logo*
  
  * *~~感谢东一手抓饼让我在周二上机课前能吃上饭~~*
  
    








