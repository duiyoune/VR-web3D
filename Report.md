## Report for 3D Runner Game in VR

一般包括用了什么技术、框架，主要工程模块的功能描述，达到的最终结果的简单表述等等。



### 基本介绍

本项目是一个基于Web3D的跑酷类VR游戏。在游戏中，玩家可以操纵小球进行左右移动，并躲避路上的障碍。由于采用了3D框架，玩家可以用鼠标调整视角。在实现过程中，主要采用了a-frame框架来完成3D场景的搭建。

<img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618135313652.png" alt="image-20210618135313652" style="zoom:50%;" />

### 框架介绍

A-Frame 是一个用来构建虚拟现实（VR）应用的网页开发框架。由WebVR的发起人Mozilla VR 团队所开发，是当下用来开发WebVR内容主流技术方案。WebVR是一个完全开源的项目，已成长为领先的VR社区。

A-Frame基于HTML，容易上手。但是A-Frame不仅仅是一个3D场景渲染引擎或者一个标记语言。其核心思想是基于Three.js来提供一个声明式、可扩展以及组件化的编程结构。

A-Frame支持主流VR头显如Vive, Rift, Daydream, GearVR,Cardboard, 甚至可被用于增强现实（AR）。虽然A-Frame支持全谱，A-Frame的目标是定义具有位置跟踪和操控的完全身临其境和交互式VR体验，超出基本的360° 内容呈现。



### 功能模块

+ 3D场景搭建

  本场景主要构成组件有天空、海洋、浮冰、冰面、障碍物与小球。由于海洋结构较为复杂，我们采用了内置开源代码的方式来实现海洋的结构与漂浮运动。除此之外，其余结构都由a-frame框架构成。

  对于绝大多多数场景，我们都通过<a-animation>标签添加上了动态运动与光影效果。部分实现代码如下所示：

  **光源**：

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618141033801.png" alt="image-20210618141033801" style="zoom:50%;" />

  **浮冰**：

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618141109417.png" alt="image-20210618141109417" style="zoom:50%;" />

  **障碍物**：

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618141242695.png" alt="image-20210618141242695" style="zoom:50%;" />

  

+ 小球控制模块

  本模块负责控制小球的运动。我们可以通过a、d按键或者左右按键来控制小球的左右移动来躲避障碍物。同时，我们实现了在该游戏在手机端的适配。即通过手机旋转角度来判断左右移动。

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618144829831.png" alt="image-20210618144829831" style="zoom:50%;" />

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618144853786.png" alt="image-20210618144853786" style="zoom:50%;" />

+ 障碍物生成模块

  我们通过设定三条赛道，并在赛道上随机生成障碍物的方式来完成地图的设计。这种设计方案可以确保每次运行都能生成不同的地图，提高可玩性。同时，设定障碍物由远及近运动，将玩家与摄像机固定，可以构造出玩家在向前运动的视觉效果。这样的方案可以减少计算量。

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618145055211.png" alt="image-20210618145055211" style="zoom:50%;" />

+ 碰撞检测模块

  当小球与障碍物碰撞时即游戏结束。我们通过检测如下条件：``POSITION_Z_LINE_START < position.z && position.z < POSITION_Z_LINE_END && tree_position_index == player_position_index``来判断小球是否撞上了障碍物。即小球的z轴位置在和障碍物的z轴体积重合，且小球在该障碍物的赛道内，即可完成碰撞判断。相比传统的碰撞检测，这种方式的计算量更小，通过先验知识来降低了程序的运算量，提高响应速度。代码如下：

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618145452791.png" alt="image-20210618145452791" style="zoom:50%;" />

+ 记分板模块

  每越过一个障碍物，记分板就会加一分。当物体撞上障碍物后记分结束，显示Game Over

  <img src="/Users/chenzijie/Library/Application Support/typora-user-images/image-20210618145627946.png" alt="image-20210618145627946" style="zoom:50%;" />



