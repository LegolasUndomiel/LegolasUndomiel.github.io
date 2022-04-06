---
title: 2013-Rivallant-Failure analysis of CFRP laminates
date: 2022-04-06 10:38:08
tags:
---

## Experimental validation of modeling

>Impact tests were performed in a drop tower system with a 2 kg – 16 mm diameter impactor, as per Airbus Industries Test Method (AITM 1–0010) [36].
>The specimens tested were 100 x 150 x 4.16 mm rectangular plates simply supported by a boundary condition of a 75 x 125 mm window.
>The laminated plate is manufactured with 0.26 mm thick T700/M21 unidirectional carbon/epoxy plies, with stacking sequence [0,45,90,45].
>This stacking sequence was chosen in order to reduce computational time by using double plies during the development of the model.
>The authors assume that mechanisms leading to the final rupture of the plate in CAI are the same whatever the ply thickness and orientation within a relatively wide range: the combination of bending stress due to buckling and compressive stress concentration leading to fiber failure, as mentioned in a number of recent experimental works [37–40].

根据空中客车工业测试方法（AITM 1-0010）[36]，在落塔系统中用一个2公斤-16毫米直径的冲击器进行冲击测试。
**测试的试样是100x150x4.16毫米的矩形板，由75x125毫米的窗口的边界条件简单支撑。**
层压板是用0.26毫米厚的T700/M21单向碳/环氧树脂层制造的，堆叠顺序为[0,45,90,45]。
选择这个堆积序列是为了在模型开发过程中通过使用双层板来减少计算时间。
作者假设在CAI中导致板材最终破裂的机制是相同的，无论层板的厚度和方向在一个相对宽的范围内：屈曲导致的弯曲应力和压缩应力集中导致纤维失效的组合，这在最近的一些实验工作中提到[37-40]。

>CAI tests were then performed on a hydraulic machine, the specimen being stabilized by a 90 * 130 mm window, as per Airbus Industries Test Method (AITM 1-0010) [36].

然后在液压机上进行CAI测试，根据空客工业测试方法（AITM 1-0010）[36]，试样由90*130毫米的窗口稳定。

>The composite plates were tested experimentally and numerically, at 1.6, 6.5, 17, 26.5 and 29.5 J of impact energy, and the corresponding CAI tests were performed.
>The simulation was performed in three steps (Fig. 4). The first step corresponds to the impact test, with the plate simply supported by a 75 x 125 mm window.
>This step lasted about 5 ms.
>At the end of this step, the impact damage was obtained, in particular permanent indentation.
>The second step consists in the stabilization of oscillations due to impact and the modification of the boundary conditions to set up those of CAI: the knife edges and grips were introduced and progressively moved towards the plate like in experimental tests.
>Finally, the third step consists in the CAI step, with an imposed displacement of one grip until the final fracture of the plate.
>As the model was simulated using an explicit code, the grip displacement speed was chosen at 3.75 m/min to reduce CPU time.
>It is far greater than the experimental value, but a study on the influence of this speed on the CAI simulation results showed the relevance of the choice.
>The total calculation time of this model is between 12 and 15 h – depending on the impact energy level – with 8 CPUs and without optimization of the modeling to decrease this time.

在1.6、6.5、17、26.5和29.5J的冲击能量下，对复合材料板进行了实验和数值测试，并进行了相应的CAI测试。
模拟分三步进行（图4）。第一步对应于冲击试验，板子由一个75x125毫米的窗口简单支撑。
**这一步持续了大约5毫秒**。
在这一步结束时，获得了冲击损伤，特别是永久压痕。
第二步是稳定冲击引起的振荡，修改边界条件以建立CAI的边界条件：引入刀刃和抓手，并像实验测试中那样逐渐向板块移动。
最后，第三步是CAI步骤，强加一个抓手的位移，直到板块的最终断裂。
由于该模型是用显式代码模拟的，为了减少CPU时间，抓手位移速度被选择为3.75米/分钟。
它远远大于实验值，但对这一速度对CAI模拟结果的影响的研究表明了这一选择的相关性。
这个模型的总计算时间在12到15小时之间--取决于冲击能量水平--使用8个CPU，没有优化建模以减少这个时间。

### Numerical and experimental comparison of impact tests

>The comparison between the delamination areas and the force–displacement curves obtained numerically and experimentally are shown in Fig. 5.
>It should be noted in this figure that an experimental problem did not allow us to obtain the 17 J curve.
>Globally, the fact of taking into account the rupture in compression in the fiber law does not significantly change the results on the curves and damage compared to results previously presented ([24,25]).
>In the whole range of energies considered, a relatively good correlation is observed between modeling and experiments; the shape and size of the delaminated interfaces are well simulated (Figs. 5 and 6), even if the area of the first interface, non-impacted side, is overestimated for the highest energies.
>The simulated force–displacement curves take into account the different stiffness decreases: the first one at about 2 mm-displacement is soft and mainly due to delamination, and the second one, at about 5 mm-displacement, is strong and mainly due to fiber failure.
>Permanent indentation is also well represented (Fig. 6); this highlights the relevance of the ‘‘like-plasticity’’ model used for matrix crack closure.

图5显示了分层面积以及通过数值和实验获得的力-位移曲线之间的比较。
在这个图中应该注意到，一个实验问题不允许我们获得17J的曲线。
总的来说，在纤维法中考虑到压缩中的断裂这一事实，与以前提出的结果相比（[24,25]），对曲线和损伤的结果没有明显的改变。
在所考虑的整个能量范围内，在建模和实验之间观察到了相对较好的相关性；分层界面的形状和尺寸被很好地模拟出来（图5和图6），即使第一个界面，非冲击侧的面积在最高能量下被高估了。
模拟的力-位移曲线考虑到了不同的刚度下降：第一个大约2毫米位移的刚度是软的，主要是由于分层，第二个，大约5毫米位移的刚度是强的，主要是由于纤维失效。
永久压痕也得到了很好的体现（图6）；这突出了用于基体裂缝闭合的 "相似塑性 "模型的相关性。

>Even if the new law for fiber failure in compression does not lead to significant differences in the global behavior of the plate (curves and delamination areas), it enables the presence of compression cracks, as can be observed after 29.5 J impact simulation in the central zone under the impactor (Fig. 7), to be taken into account.
>It can be noticed in Fig. 7 that only the half-plate is drawn and that the deformed shape is free of exterior loads and then only due to the ‘‘like-plasticity’’ model in the matrix cracking elements mentioned above.
>Most fiber failures are due to tension failures and only the zone just under the impactor, impacted side, presents some compression failures.
>However, a fiber failure crack in compression is also observed on the impacted side right next to the point of impact (Fig. 7).
>This crack only concerns the first 0 ply, impacted side.
>Of course, due to the symmetry of the modeling, this crack exists ‘‘virtually’’ on the other half-plate.
>This crack turns out to be of utmost importance during CAI because its propagation induces the final fracture of the plate.
>In fact, after impact tests, this crack is not so obvious on the specimens and is therefore slightly overestimated by the modeling.
>Unfortunately, as we did not look for cracks after impact tests, it is not possible to prove their presence on the specimen that we tested in CAI, but Fig. 8 shows cracks after two different static indentation tests.
>Fig. 8a is a microscopic observation of a barely visible crack (not a compression crack, but one which can propagate in compression during CAI) due to a 24.8 J static indentation, whereas Fig. 8b clearly shows the visible compression cracks due to a slightly higher energy: 27.3 J static indentation.
>For lower impact energies, it seems that the latter crack is not visible after impact on the surface of the plate.

即使纤维在压缩中失效的新规律不会导致板的整体行为（曲线和分层区域）的重大差异，它也能使压缩裂缝的存在得到考虑，正如在29.5J的冲击模拟后，在冲击器下的中心区域可以观察到的（图7）。
在图7中可以注意到，只有半板被画出来，变形的形状是没有外部载荷的，然后只是由于上面提到的矩阵裂纹元素中的''相似塑性''模型。
大多数纤维失效是由于张力失效，只有在冲击器下面的区域，即被冲击的一侧，呈现一些压缩失效。
然而，在紧挨着撞击点的被撞击一侧也观察到了压缩的纤维失效裂纹（图7）。
这条裂缝只涉及到第一层的0层，被撞击的一侧。
当然，由于建模的对称性，这条裂纹 "实际上 "存在于另一个半板上。
这条裂纹在CAI过程中被证明是最重要的，因为它的扩展会诱发板的最终断裂。
事实上，在冲击试验后，这条裂纹在试样上并不明显，因此被建模稍微高估了。
不幸的是，由于我们没有在冲击试验后寻找裂纹，因此无法证明在我们进行CAI测试的试样上存在裂纹，但图8显示了在两种不同的静态压痕试验后的裂纹。
图8a是对24.8J静态压痕导致的几乎不可见的裂纹（不是压缩裂纹，但在CAI期间可以在压缩中传播）的微观观察，而图8b清楚地显示了稍高能量：27.3J静态压痕导致的可见压缩裂纹。
对于较低的冲击能量，似乎后一种裂纹在冲击板的表面后是不可见的。
