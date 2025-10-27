## 1.程序功能描述

基于UKF-IMM无迹卡尔曼滤波与交互式多模型的轨迹[跟踪算法](https://so.csdn.net/so/search?q=%E8%B7%9F%E8%B8%AA%E7%AE%97%E6%B3%95&spm=1001.2101.3001.7020)matlab仿真,对比EKF-IMM和UKF。

## 2.测试软件版本以及运行结果展示

MATLAB2022A版本运行

![1d0bfe7ef4e94ca0869a82ba2a28b57b](https://img2024.cnblogs.com/blog/3292833/202510/3292833-20251027130024055-928673806.jpg)

![2eb4af9eb2ff46c8b8f209fc22999b00](https://img2024.cnblogs.com/blog/3292833/202510/3292833-20251027130036492-280917886.jpg)

![11f4772a08934f93aa82d2b0d6c22110](https://img2024.cnblogs.com/blog/3292833/202510/3292833-20251027130042695-684621538.jpg)

![45c8a4f454f74b969e3a3b3e320a3fbc](https://img2024.cnblogs.com/blog/3292833/202510/3292833-20251027130048848-339354146.jpg)

![73878667b19744b298e4d09b50b3507f](https://img2024.cnblogs.com/blog/3292833/202510/3292833-20251027130054276-427303862.jpg)

## 3.核心程序

[?](https://github.com):[西柚加速器](https://xiyojiasu.com)

|  |  |
| --- | --- |
| 1  2  3  4  5  6  7  8  9  10  11  12  13  14  15  16  17  18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99  100  101  102  103  104  105  106  107  108  109  110  111  112  113  114  115  116  117  118  119  120  121  122  123  124  125  126  127  128  129  130  131  132  133  134 | `.............................................................................`  `% 绘制目标运动与传感器分布的图形，展示 IMM - UKF 算法的跟踪效果`  `%目标运动与传感器分布`  `figure`  `% 绘制目标的真实轨迹`  `plot(TargetState(1,:),TargetState(4,:),``'k'``,``'LineWidth'``,2);`  `hold` `on`  `% 循环处理每个节点`  `for` `i = 1:NumberNode`  `% 绘制 IMM - UKF 算法的状态估计轨迹`  `plot(Xfstate(1,:),Xfstate(4,:),``'-mo'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.5,0.9,0.0]);`  `hold` `on`  `% 绘制真实节点的位置`  `plot(NodeDistribution(1,i),NodeDistribution(2,i),``'bo'``,``'LineWidth'``,1);`  `hold` `on`  `% 在节点位置旁边标注节点编号`  `text(NodeDistribution(1,i)+0.5,NodeDistribution(2,i)+0.5,num2str(i));`  `hold` `on`  `% 绘制 IMM - UKF 算法估计的节点位置`  `plot(pest(1,i),pest(2,i),``'rs'``,``'LineWidth'``,1);`  `hold` `on`  `% 添加图例说明不同线条和标记的含义`  `legend(``'真实轨迹'``,``'IMM-UKF估计轨迹'``,``'真实节点'``,``'IMM-UKF节点'``);`  `% 设置图形标题`  `title(``'跟踪效果对比'``);`  `end`  `% 设置坐标轴为正方形，使图形比例合适`  `axis square`    `% 绘制目标运动与传感器分布的图形，展示 IMM - EKF 算法的跟踪效果`  `figure`  `% 绘制目标的真实轨迹`  `plot(TargetState(1,:),TargetState(4,:),``'k'``,``'LineWidth'``,2);`  `hold` `on`  `% 循环处理每个节点`  `for` `i = 1:NumberNode`  `% 绘制 IMM - EKF 算法的状态估计轨迹`  `plot(Xfstate2(1,:),Xfstate2(4,:),``'-mo'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.5,0.9,0.0]);`  `hold` `on`  `% 绘制真实节点的位置`  `plot(NodeDistribution(1,i),NodeDistribution(2,i),``'bo'``,``'LineWidth'``,1);`  `hold` `on`  `% 在节点位置旁边标注节点编号`  `text(NodeDistribution(1,i)+0.5,NodeDistribution(2,i)+0.5,num2str(i));`  `hold` `on`  `% 绘制 IMM - EKF 算法估计的节点位置`  `plot(pest2(1,i),pest2(2,i),``'rs'``,``'LineWidth'``,1);`  `hold` `on`  `% 添加图例说明不同线条和标记的含义`  `legend(``'真实轨迹'``,``'IMM-EKF估计轨迹'``,``'真实节点'``,``'IMM-EKF节点'``);`  `% 设置图形标题`  `title(``'跟踪效果对比'``);`  `end`  `% 设置坐标轴为正方形，使图形比例合适`  `axis square`    `% 绘制目标运动与传感器分布的图形，展示 UKF 算法的跟踪效果`  `figure`  `% 绘制目标的真实轨迹`  `plot(TargetState(1,:),TargetState(4,:),``'k'``,``'LineWidth'``,2);`  `hold` `on`  `% 循环处理每个节点`  `for` `i = 1:NumberNode`  `% 绘制 UKF 算法的状态估计轨迹`  `plot(Para_sensor3(1,:),Para_sensor3(4,:),``'-mo'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.5,0.9,0.0]);`  `hold` `on`  `% 绘制真实节点的位置`  `plot(NodeDistribution(1,i),NodeDistribution(2,i),``'bo'``,``'LineWidth'``,1);`  `hold` `on`  `% 在节点位置旁边标注节点编号`  `text(NodeDistribution(1,i)+0.5,NodeDistribution(2,i)+0.5,num2str(i));`  `hold` `on`  `% 绘制 UKF 算法估计的节点位置`  `plot(pest3(1,i),pest3(2,i),``'rs'``,``'LineWidth'``,1);`  `hold` `on`  `% 添加图例说明不同线条和标记的含义`  `legend(``'真实轨迹'``,``'UKF估计轨迹'``,``'真实节点'``,``'UKF节点'``);`  `% 设置图形标题`  `title(``'跟踪效果对比'``);`  `end`  `% 设置坐标轴为正方形，使图形比例合适`  `axis square`    `% 绘制不同算法的误差随时间变化的曲线`  `figure`  `% 绘制 IMM - UKF 算法的误差曲线`  `plot(tms,err1(1,:),``'-bs'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.9,0.0,0.0]);`  `hold` `on``;`  `% 绘制 IMM - EKF 算法的误差曲线`  `plot(tms,err2(1,:),``'-mo'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.5,0.9,0.0]);`  `hold` `on``;`  `% 绘制 UKF 算法的误差曲线`  `plot(tms,err3(1,:),``'-r>'``,...`  `'LineWidth'``,1,...`  `'MarkerSize'``,6,...`  `'MarkerEdgeColor'``,``'k'``,...`  `'MarkerFaceColor'``,[0.9,0.9,0.0]);`  `hold` `on``;`  `% 添加图例，说明不同曲线对应的算法`  `legend(``'IMM - UKF '``,``'IMM - EKF'``,``'UKF'``);`  `% 设置 x 轴标签为时间步`  `xlabel(``'Time Steps'``)`  `% 设置 y 轴标签为误差`  `ylabel(``'error'``)`    `% 绘制不同算法的平均误差柱状图`  `figure`  `% 绘制三个算法的平均误差柱状图`  `bar([mean(err1(1,:)),mean(err2(1,:)),mean(err3(1,:))]);`  `% 设置 x 轴标签，说明每个柱子对应的算法`  `xlabel([``'1:IMM - UKF, 2:IMM - EKF, 3:UKF'``]);`  `% 设置 y 轴标签为误差`  `ylabel(``'error'``)`  `93` |

## 4.本算法原理

在许多工程实践中，往往不能直接得到所需要的状态变量的真实值。例如雷达在探测目标时，可以通过回波信号等计算出目标的距离、速度和角度等信息。但雷达探测过程中会存在干扰（系统噪声、地杂波和非目标信号等）的问题，这些干扰会导致回波信号中夹杂有随机噪声。我们要在有随机噪声的回波信号中分离目标的运动状态量，准确的得到这个状态量往往是不可能的，只能根据观测信号估计这些状态变量。卡尔曼滤波就是这种通过估计或预测降低噪声影响的一种好的方法。特别是在线性系统中，卡尔曼滤波是最优的滤波算法。

在轨迹跟踪问题中，系统状态通常随时间变化，并且受到过程噪声的影响；同时，对系统状态的观测也包含观测噪声。我们的目标是根据一系列的观测值来估计系统的真实状态。UKF 是一种用于非线性系统状态估计的滤波算法。与传统的扩展卡尔曼滤波（EKF）不同，UKF 不依赖于对非线性函数的线性化，而是通过一组确定性采样点（Sigma 点）来近似状态的概率分布，从而更准确地处理非线性问题。

在kalman滤波算法中用到了状态转移方程和量测方程，被估计量随着时间的变化，呈现的是一个动态估计。在目标跟踪中，不需要知道目标的运动模型就能实时的修正目标的状态变量（速度、距离等），具有良好的适应性。但是当目标实施机动变化（突然加、减速或急转弯等），仅仅采用基本的kalman滤波算法往往得不到理想的结果。这时就需要采用自适应算法。交互多模型（IMM）就应用而生。

　　目标交互多模型kalman滤波算法在机动目标跟踪领域得到广泛应用。IMM算法使用两个或者多个模型来描述工作过程中可能出现的状态，最后通过有效的加权融合进行系统状态估计，很好的克服了单个模型估计误差较大的问题。

IMM 算法用于处理系统在不同模式下运行的情况。它假设系统存在多个可能的运行模式，每个模式对应一个不同的状态模型，通过在这些模型之间进行交互和切换，以适应系统模式的变化，从而提高状态估计的准确性。

![1dcf6289b03441258413feb8de4a3f89]()

![24f3b95bbc844bcaacc3e1b30140825b]()

![91b193aad54743afb0b6cc9e0b58ddbb]()

![01479c676ee448beb2b47bd2d85bc450]()

![31561d3e140c4ddf9dff1e4e55b83663]()

## 5.完整程序

VVV
