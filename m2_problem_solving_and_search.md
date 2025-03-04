# 问题解决和搜索

## 模块概览

本模块名为问题解决和搜索（Problem Solving and Search），将会讲述AI领域对于问题解决（Problem Solving）常见的搜索算法（Search Algorithm）。

对于AI领域的常见搜索算法，我们可以将它分为两个大类，**系统性的状态空间搜索（Systematic State-space Search）**和**本地搜索（Local Search）**。

其中，系统性的状态空间搜索（Systematic State-space Search）又包含两类：

- 不知情搜索（Uninformed Search），又称盲搜（Blind Search）；
- 知情搜索（Informed Search），又称启发式搜索（Heuristic Search）。

![search_algorithms_CN_EN](../images/m2_search_algorithms_CN_EN.png)

在悉尼大学的COMP3308的教学计划中：

- Week 2将讲述：不知情搜索（Uninformed Search）的5种算法，知情搜索算法（Informed Search）的2种算法中的第一种 —— 贪心最佳优先（Greedy best-first）；
- Week 3将讲述：知情搜索（Informed Search）的2种算法中的第二种 —— A*，本地搜索（Local Search）的4种算法。

看到这的小伙伴可能会对上面这一系列算法术语有点懵，没关系，以上只是便于你做大作业前、或学完整学期期末考前倒回来寻找对应知识点的模块概览。

本模块将会在开始的第一节 - *人工智能中问题解决的常见搜索算法的分类*用生动形象、简单易记的比喻告诉你这些算法的区别；然后将在接下来的每节逐一讲解上述三类、共11种的搜索算法、并辅以配套练习，便于同学们直接完成学以致用。

---

## 人工智能中问题解决的常见搜索算法的分类

### 通过比喻情景来解释：AI中问题解决的搜索算法分类

![search_algorithms_CN_EN](../images/m2_search_algorithms_CN_EN.png)

下面的表格通过**两种便于同学们理解的比喻情景（也是两种AI搜索算法可能的实用场景）**，帮助同学们理解什么是系统性的状态搜索（Systematic State-space Search）下的不知情搜索（Uninformed Search）和知情搜索（Informed Search），什么是本地搜索（Local Search）。

| 比喻情景/可能 <br> 的实用场景 | 不知情搜索 (盲) <br> Uninformed Search (Blind) | 知情搜索 （启发式）<br> Informed Search (Heuristic) | 本地搜索 <br> Local Search |
| :---------------- | :------  | :----  | :---- |
| 公路旅行           | 拿着地图系统性检查每条路， <br> 每逢岔路口，都是按算法固定 <br> 顺序穷举尝试每条路，遇到死 <br> 胡同或受到算法限制时返回上 <br> 级，直到抵达目的地。 | 同为拿着地图系统性尝试，但每逢 <br> 岔路口尝试路的先后顺序更优化， <br> 按某种有意义的启发性提示判断， <br> 如哪条路角度更接近目的地方向则 <br> 优先尝试，遇到死胡同或受算法限 <br> 制时返回上级，直到抵达目的地。 | 没有地图，每逢岔路口 <br> 都根据路标和周围环境 <br> 判断走哪条路，以期待 <br> 能抵达目的地。 |
| 侦探找嫌疑人    |  侦探不放过所有现场线索，将 <br> 关系网内所有可能的嫌疑人按 <br> 算法固定的顺序穷举法进行调 <br> 查，遇到排除者或受算法限制 <br> 时返回上级，直到抓住真犯。  | 同为不放过所有现场线索，但在关 <br> 系网内对嫌疑人调查的先后顺序更 <br> 优化，按某种有意义的启发性提示 <br> 进行判断，如案发时距离现场近的 <br> 优先调查，遇到排除者或受算法限 <br> 制时返回上级，直到抓住真犯。 | 没有关系网，每调查一 <br> 个嫌疑人，就根据ta的 <br> 陈述和对ta的调查，判 <br> 断调查哪个跟ta有连带 <br> 关系的人，以期待找到 <br> 真犯。 |
| **总结**    |  **不知情搜索（Uniformed**  <br> **Search）一般会对整个状态** <br> **空间（state-space）进行** <br> **搜索，大部分能找到全局最优** <br> **解，少部分会陷入循环或找到** <br> **局部最优解而错过全局最优。**   | **知情搜索（Informed Search）** <br> **一般会对整个状态空间（state-** <br> **space）按启发性提示（heuristic）** <br> **进行搜索，贪心最佳优先（Greedy** <br> **best-first）可能找到局部最优而错** <br> **过全局最优，A*能找到全局最优。** | **因仅探索临近而非全局** <br> **状态，而占用状态空间** <br> **小（空间复杂度低），** <br> **虽不系统但特定情况有** <br> **奇效，易卡死在死胡同** <br> **而无解，或找到局部最** <br> **优错过全局最优。** |
| 具体算法    |  1. 广度优先 Breadth-first <br> 2. 统一成本 Uniform cost <br> 3. 深度优先 Depth-first <br> 4. 深度受限 Depth-limited <br> 5. 迭代深度递增 <br> Iterative-deepening  | 1. 贪心最佳优先 Greedy best-first <br> 2. A*  | 1. 爬山 Hill-climbing <br> 2. 束搜索 Beam search <br> 3. 模拟退火 <br> Simulated annealing <br> 4. 遗传 Genetic |

上表的三类（Informed Search、Uninformed Search、Local Search）共11种的搜索算法，将在具体的知识点中逐一讲解，并配合配套练习让同学们直接学以致用。

其中，在上表对本地搜索（Local Search）的总结中提到“虽不系统但特定情况下有奇效”，这当中所说的“特定情况”是指一类特定的**Optimization Problems**的Problem Solving，详见：*优化问题的定义和构建（Optimization Problems - Definition and Formulation）*。

---

## 问题解决（Problem Solving）和搜索问题（Search Problem）

### Problem Solving中适合转化为搜索问题（Search Problem）解决的场景

在AI被运用于问题解决中时，如一个问题可以被明确表示出初始状态（Initial State）和目标状态（Goal State）、并且以初始状态开始进行的变化的中间步骤可以同样被**抽象**（**Abstraction**）变为一个个中间的状态（State）时，则这个问题大概率适合被转化为搜索问题。包括但不限于：

- 飞机/高铁/地铁等购票过程中，忽略掉进站、出站、安检等细节，将每一个站作为state，根据对应要求设定首发站为initial state、终点站为goal state，再进行搜索。
- 下中国象棋/国际象棋/围棋等各类棋的过程中，忽略到拿子、落子等细节，将当前的棋盘布局作为state，根据对应要求设定初始的棋盘布局为initial state、能达成一方获胜的判定的任何棋盘布局作为goal state。

### 搜索问题的构建（Search Problem Formulation）

搜索问题由4项来构建：

- **初始状态（Initial state）**
- **目标状态（Goal state）**
- **运算符（Operators = actions）**
- **路径成本函数（Path cost function）**

搜索问题的构建需要关注问题解决的核心方面，对**抽象**（**Abstraction**）十分依赖，抽象则要求忽略掉一些不重要的细节，侧重解决一个问题的主要部分，比如：当我们思考怎么将“通过乘坐民航飞机的形式从中国广州到澳大利亚悉尼”这个问题抽象成搜索问题时，我们则：

- （**关于abstraction**）需忽略掉打车去机场、办理登机牌、托运行李等步骤（典型的抽象掉细节）。
- （**关于states**）将广州这个城市设为初始状态（Initial State）；悉尼这个城市设为目标状态（Goal State）；转机的中转站（如印尼的巴厘岛、马来西亚的吉隆坡等）设置为中间的状态（Possible Intermediate State）。
- （**关于operators/actions**）将从一个城市飞往另一个城市的行为（action）作为运算符（operator），例如：从广州飞往吉隆坡、从吉隆坡飞往悉尼。
- （**关于path cost function**）：将问题解决所要求的path cost设置为function，包括但不限于：
  - 考虑有无机票预算要求，将机票和基建燃油的费用模拟成从一个城市/state到另一个城市/state的路径成本（path cost）；
  - 或考虑有无航行总时间要求，将每段航程的时间设置成另一种path cost；
  - 又或者考虑直飞或转机次数小于几次，则会对搜索算法的层数进行限制，当转机数有限制时，转机一次也可以设置为path cost = 1。
  
  因此，对于path cost的设置完全取决于用户（user）的要求，例如：我们在看上购票软件上，常见地发现，当筛选条件不同时，推荐购买的票的优先级排序则不一样。

目标状态（Goal State）则有时可以不只有一个，下面给两种例子，如：

- 例子一 - **多个可在一开始确定的Goal States (显性阐述，stated explicitly)**：<br> 延续上面的案例、略作修改，我们还是从中国广州、**但目标从仅澳大利亚悉尼改为到达澳大利亚（不限制城市）**，则此时所有澳大利亚的有国际航班抵达的机场的城市都将成为多个确定的Goal States。
- 例子二 - **多个难以在一开始穷举确定、却能够通过条件判断的Goal States (隐性阐述，stated implicitly with a goal test)**：<br> 当我们在下中国象棋、国际象棋时，都是从一个固定的棋盘布局作为Initial State开始，但是我们对达成Goal State的判定是**将军（Check）且对方无法通过移动任何棋子救场**（救场包括：移动将/帅/王跑路避开将军、挡住或吃掉将军的棋子），即对方被“**将死了**”（**Checkmate**）。中国象棋要求一方将对方的将（黑）/帅（红）“将死了”为胜；国际象棋要求一方将对方的王“将死了”为胜。此时，**任何符合一方将对方“将死了”的目标判断（goal test）的棋盘布局**都将成为Goal States。

### 边缘（Fringe）和展开的结点（Expanded Nodes）

假设同学们都已经具有初步的数据结构与算法的基础，下面以BFS、DFS进行举例，讲解两个search problem中

以BFS为例，讲解AI。。。search。。

### 搜索策略（Search Strategy）的定义与衡量标准

- Completeness – is it guaranteed to find a solution if one exists?
- Optimality – is it guaranteed to find an optimal (least cost path) solution?
- Time complexity – how long does it take to find the solution? (measured as
number of generated nodes)
- Space complexity 
---

## 不知情搜索（Uninformed Search，Blind）

### 不知情搜索（Uninformed Search，Blind）的定义



### 广度优先搜索（Breadth-first Search，BFS）



### 统一成本搜索（Uniform Cost Search，UCS）

### 深度优先搜索（Depth-first Search，DFS）

### 深度受限搜索（Depth-limited Search）和迭代深度递增搜索（Iterative-deepening Search，IDS）

---

## 知情搜索（Informed Search，Heuristic）

### 知情搜索（Informed Search，Blind）的定义

### 贪心最佳优先搜索（Greedy  Best-first Search）

### A\*搜索（A* Search）

---

## 优化问题（Optimisation Problems）和本地搜索（Local Search）

### 优化问题的定义和构建（Optimization Problems - Definition and Formulation）

### 爬山（Hill-climbing）

### 束搜索（Beam search）

### 模拟退火（Simulated annealing）

### 遗传算法（Genetic Algorithm）

