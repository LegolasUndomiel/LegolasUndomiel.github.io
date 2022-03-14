---
title: 2018-Bogenfeld-Review and benchmark
date: 2022-03-14 15:07:33
tags:
---

>## Review and benchmark study on the analysis of low-velocity impact on composite laminates
>
>低速冲击对复合材料层压板分析的回顾和基准研究

- **Author**
  - Raffael Bogenfeld
  - Janko Kreikemeier
  - Tobias Wille

## Abstract

>For the analysis of low-velocity impact damage, many analytical and numerical models were developed by various authors.
>These models range from simple approaches with a single degree of freedom up to finite element models on micro-scale.
>The prediction of delamination, fiber failure, and inter-fiber damage, as well as a physically sound kinematic behavior, are usually the objectives of these simulations.
>However, achieving satisfactory results requires massive computation and modeling efforts.
>In the present paper, we review the capability to capture impact damage on the coupon and the structural level.
>For this purpose, a large compendium of analytical and numerical analysis methods from various authors is considered.
>Based on existing works, six representative modeling approaches of different abstraction scales are derived and considered on a qualitative and quantitative benchmark study.
>We analyze all models regarding their advantages and deficiencies.
>With two experimental coupon impacts, all approaches are tested on their predictive capabilities on the coupon level.
>The applicability of these methods on the structural level is evaluated according to the benchmark results.
>Modeling approaches included in the benchmark range from high-fidelity models on meso-scale, macro-scale shell models, and analytical estimations.
>The focus is put on stacked layer models with solid or shell elements and various cohesive zone approaches.
>The energy distribution over the eigenmodes of the impact system suitably indicates the limit of low-velocity impact.

为了分析低速冲击损伤，不同的作者开发了许多分析和数值模型。
这些模型从单一自由度的简单方法到微观尺度的有限元模型。
**预测分层、纤维断裂和纤维间损伤，以及物理上合理的运动行为，通常是这些模拟的目标。**
然而，取得令人满意的结果需要大量的计算和建模工作。
在本文中，我们回顾了捕捉试样和结构层面的冲击损伤的能力。
为此，我们考虑了来自不同作者的大量分析和数值分析方法的汇编。
在现有工作的基础上，得出了六种不同抽象尺度的代表性建模方法，并在定性和定量的基准研究中进行了考虑。
我们分析了所有模型的优点和不足。
通过两个实验券的影响，测试了所有方法在券面上的预测能力。
根据基准结果，这些方法在结构层面的适用性得到了评估。
基准中包括的建模方法有中尺度的高保真模型、宏观尺度的壳模型和分析估算。
**重点放在具有实体或壳元素的堆积层模型和各种粘着区方法**。

>With this paper, we also present guidelines for impact analysis strategies on the structural level.
>These guidelines aim for a good balance between accuracy and computation effort and involve various simplifications of impact scenarios.
>In this regard, the range of low-velocity has to be monitored.

通过这篇论文，我们还提出了结构层面上的影响分析策略指南。
这些指导原则的目的是在准确性和计算工作量之间取得良好的平衡，并涉及到对冲击情况的各种简化。
在这方面，必须监测低速的范围。
冲击系统的特征模式的能量分布适当地表明了低速冲击的极限。

## Introduction

>Composite structures are likely to be exposed to impact loads during their service life.
>Bird strike, hail or tool-drop are typical examples of an impact on an aircraft structure.
>Usually, impact scenarios are distinguished between Low-Velocity Impact (LVI), High Velocity Impact (HVI) and ballistic impact.
>Among these, LVI is of particular importance for the structural lifetime.
>LVI causes damage inside the material, consisting mainly of delamination [1,2].
>Such damage is classified as a Barely Visible Impact Damage (BVID).
>If no other visible damage-modes occur simultaneously the damage will possibly remain undetected.
>Even though a significant strength reduction is possible [3], the structure still has to stay capable of bearing the design loads.
>Sufficient residual strength needs to be ensured for the entire structural lifetime.
>This problem is often approached by a massive qualification effort with tests on structures and coupons.
>Besides, conservative knock-down factors increase the designed thickness of structures.
>In consequence, the significant advantage of a fiber reinforced material — a lightweight design — nearly disappears.
>Thus, derivation of design improvements by the aid of numerical analysis becomes attractive.

**复合材料结构在其使用寿命中可能会受到冲击载荷的影响**。
**鸟击、冰雹或工具坠落是对飞机结构产生冲击的典型例子**。
通常情况下，撞击情况分为低速撞击（LVI）、高速撞击（HVI）和弹道撞击。
**其中，LVI对结构寿命特别重要。**
LVI导致材料内部的损坏，主要包括分层[1,2]。
**这种损伤被归类为几乎不可见的冲击损伤（BVID）。**
**如果没有其他可见的损伤模式同时发生，那么这种损伤就有可能不被察觉。**
**即使有可能出现明显的强度下降[3]，结构仍然必须保持能够承受设计载荷。**
**足够的剩余强度需要在整个结构寿命中得到保证。**
**这个问题通常是通过对结构和试样进行大规模的鉴定工作来解决的。**
**此外，保守的推倒系数增加了结构的设计厚度。**
**因此，纤维增强材料的重要优势--轻质设计--几乎消失了。**
因此，借助于数值分析来推导设计的改进变得有吸引力。

>Impact analysis on composite structures has already been a topic of research since the early nineties [4].
>Many models that vary in abstraction scale and applied methods were proposed for the last ten years.
>Recent studies show that it is possible to obtain excellent simulation results through meso-scale finite element models.
>However, the simulation of impact is still challenging from the numerical point of view.
>Achieving a sufficient accuracy in a reasonable computation time remains a challenge.
>For coupon simulations with state-of-the-art models, computation times of one day or more are reported [3,5].
>LVI is for one reason mainly critical here: a high impactor-mass mi results in long contact time — this time needs to be captured by a transient simulation.
>The computation time increases approximately linearly with the impact duration and is consequently proportional to mi.

自90年代初以来，对复合材料结构的冲击分析已经成为一个研究课题[4]。
在过去的十年中，人们提出了许多不同的抽象尺度和应用方法的模型。
最近的研究表明，通过中尺度的有限元模型有可能获得出色的模拟结果。
然而，从数值的角度来看，冲击的模拟仍然是一个挑战。
在合理的计算时间内达到足够的精度仍然是一个挑战。
据报道，用最先进的模型进行券模拟，计算时间为一天或更长[3,5]。
LVI在这里主要是出于一个原因：高冲击器-质量mi导致长的接触时间--这个时间需要通过瞬态模拟来捕捉。
计算时间与撞击持续时间呈近似线性增长，因此与mi成正比。

>Existing reviews on impact simulation rather focus on details of a selected modeling approach, such as the variation of failure conditions or damage model.
>With the present work, the authors intend to compare methods in a more general way.
>A juxtaposition of models on different abstraction scales shall provide the groundwork for weighing up the analysis effort and the result quality of an impact analysis.

**现有的关于冲击模拟的评论更多的是集中在某个选定的建模方法的细节上，如失效条件的变化或损伤模型。**
通过这项工作，作者打算以一种更普遍的方式来比较各种方法。
不同抽象尺度上的模型并列，将为权衡分析工作和冲击分析的结果质量提供基础。

>For that purpose, we introduce the methods available in the literature and explain the corresponding modeling techniques and fundamental equations briefly.
>On the basis of the available methods, a choice of six specific methods is made.
>These shall cover a wide range of abstraction scales and analysis efforts.
>So, we chose two analytical and four finite element approaches which are all differently costly concerning the model preparation and the result computation.

为此，我们介绍了文献中现有的方法，并简要解释了相应的建模技术和基本方程。
在现有方法的基础上，我们选择了六种具体方法。
这些应涵盖广泛的抽象尺度和分析工作。
因此，我们选择了两种分析方法和四种有限元方法，它们在模型准备和结果计算方面的成本都不同。

>All models are based on existing publications.
>Partially, modifications or recombinations were required to ensure their comparability.
>An evaluation of the methods is conducted through analyzing the predictive capabilities, the modeling effort, and the computational expenses.
>In the actual benchmark, a direct comparison with the help of two test examples is presented.
>This comparison relies on experimental data and allows to evaluate the models' performance.
>Based on the benchmark results, guidelines for impact analysis on the structural level are derived.
>Several suggested simplifications and idealizations of impact scenarios shall improve the efficiency of impact analysis on the structural level.

所有模型都是基于现有的出版物。
部分需要修改或重新组合以确保其可比性。
通过分析预测能力、建模工作和计算费用，对这些方法进行了评估。
在实际的基准中，在两个测试例子的帮助下进行了直接比较。
这种比较依赖于实验数据并允许评估模型的性能。
基于基准结果，得出了结构层面上的影响分析准则。
一些建议的简化和理想化的冲击方案将提高结构层面的冲击分析的效率。

## Review of developments in impact analysis

### Steps of development

>The development of impact analysis methods went from simple analytical models to high-fidelity finite element approaches.
>The overview in Fig. 1 shows the range of methods considered in this review.
>Each increase of predictive capabilities means a simultaneous increase of the analysis effort.
>The major aim of impact analysis is the prediction of damage.
>Already analytical or empirical expressions can provide information about the damage onset and its quantitative dimensions.
>Numerical models can predict the damage type and shape, depending on the modeling strategy with a different degree of detail.

冲击分析方法的发展从简单的分析模型到高保真的有限元方法。
图1中的概述显示了本评论所考虑的方法范围。
预测能力的每一次提高都意味着分析工作量的同时增加。
**冲击分析的主要目的是预测损伤**。
已有的分析性或经验性表达式可以提供关于损伤发生和其定量的信息。
数值模型可以预测损伤的类型和形状，这取决于具有不同程度细节的建模策略。

>Early analytical methods treat an impact system as a multi-body system in which springs connect one or more masses.
>Abrate published the first of such spring-mass models in 1991 [4], and later by Christoforou [6] and others followed.
>These models capture an elastic impact response, taking into account the plate deformation of the structure and the local surface indentation.
>Based on a spring-mass model, Christoforou even developed a semi-analytical approach for analyzing impact by dimensionless constants, the socalled loss factor theory [7].
>It allows achieving kinematic similarity of size-scaled impact scenarios.
>These analytical methods permit an estimation of impact duration, maximum contact force, and impactor displacement.
>Furthermore, Olsson developed an advanced spring-mass model [8,9] that captures damage by a spring in series with the bending deformation.
>Singh and Mahajan [10] recently enhanced this idea through damage consideration in each deformation mode.

早期的分析方法将冲击系统视为一个**多体系统**，其中弹簧连接一个或多个质量。
Abrate在1991年发表了第一个这样的**弹簧-质量模型**[4]，后来Christoforou[6]等人又发表了。
这些模型捕捉到了弹性冲击响应，考虑到了**结构的板块变形和局部表面压痕**。
基于弹簧-质量模型，Christoforou甚至开发了一种半分析方法，通过无量纲常数来分析冲击，即所谓的损失因子理论[7]。
它允许实现大小比例的冲击场景的运动学相似性。
这些分析方法允许对撞击持续时间、最大接触力和撞击器位移进行估计。
此外，Olsson开发了一个先进的弹簧质量模型[8,9]，捕捉到弹簧与弯曲变形串联的损伤。
Singh和Mahajan[10]最近通过考虑每个变形模式中的损伤来加强这一想法。

>The next higher abstraction level is a plate model.
>This approach comprises more natural frequencies of the impact system.
>Dobyns' development on the dynamics of orthotropic plates [11] forms the basis of those approaches.
>Building on that, Olsson derived in 1992 the first impact model [12], based on Kirchhoff's plate equation.
>Besides, Swanson proposed an improved plate approach in 2005 [13] that is also valid for composite laminates [13].
>Such plate models capture the undamaged dynamic behavior with higher accuracy than spring-mass approximations.
>The inclusion of material-specific nonlinearities, as proposed by Najafi in 2016 [14], even extends this capability.

下一个更高的抽象层次是**板块模型**。
**这种方法包括冲击系统的更多自然频率**。
Dobyns关于正交板动力学的发展[11]构成了这些方法的基础。
在此基础上，Olsson于1992年根据Kirchhoff的板块方程得出了第一个冲击模型[12]。
此外，Swanson在2005年提出了一个改进的板块方法[13]，也适用于复合层板[13]。
这种板块模型以比弹簧质量近似法更高的精度捕捉未损坏的动态行为。
如Najafi在2016年提出的包含特定材料的非线性[14]，甚至扩展了这种能力。

>Both spring-mass and plate models can be combined with an empirical or analytical prediction of Damage Threshold Loads (DTL).
>Analytical estimations of the damage initiation and extent build on such DTL.
>For instance Olsson, Schoeppner and Abrate have proposed respective methods [8,9,15].
>DTL are usually derived using fracture mechanics, to predict the contact force that makes a delamination grow.
>To predict the damage extent, Jackson and Poe [16] proposed a force-based approach that calculates the largest delamination diameter.

弹簧质量和板块模型都可以与经验或分析预测的**损伤阈值载荷（DTL）**相结合。
损伤开始和程度的分析估计建立在这种DTL之上。
例如，Olsson, Schoeppner和Abrate已经提出了各自的方法[8,9,15]。
DTL通常使用断裂力学推导，以预测使分层增长的接触力。
为了预测损坏程度，Jackson和Poe[16]提出了一种基于力的方法，计算最大的分层直径。

>Beyond the possibilities of analytical description, impact analysis can be conducted by the finite element method in many variations.
>These variations are categorized in macro-, meso- and micro-models, depending on the laminate's abstraction scale of the finite elements.
>Layered-shell approaches belong to the macro-scale.
>As proposed by Elder et al. in 2003 [17], such models capture the kinematics of impact like a plate model.
>But they permit the evaluation of failure conditions on the ply-level and the corresponding stiffness degradation.
>The model by Elder used explicit simulations in LS-DYNA implementation, Baaran [18,19] and Kärger [20,21] even developed a stand-alone-tool for impact analysis (CODAC1).
>By implicit time integration, combined FE analysis, and analytical equations an efficient impact analysis was achieved.

在分析描述的可能性之外，冲击分析可以通过**有限元方法**进行许多变化。
这些变化可分为**宏观、中观和微观模型**，取决于层压板的有限元抽象尺度。
分层壳方法属于宏观尺度。
正如Elder等人在2003年提出的[17]，这种模型像板块模型一样捕捉冲击的运动学。
但它们允许评估层级上的失效条件和相应的刚度退化。
Elder的模型在LS-DYNA实现中使用了显式模拟，Baaran[18,19]和Kärger[20,21]甚至开发了一个独立的冲击分析工具（CODAC1）。
通过隐式时间积分，结合FE分析和分析方程，实现了高效的冲击分析。

>An upgraded macro-scale model that even included a stacking of sublaminates was published by Johnson et al. in 2001 [22].
>This stacking permits to use an interface model between the plies.
>Johnson applied an interface model from Allix and Ladeveze [23] to capture delamination damage.
>This method still provides the basis for state-of-the-art meso-scale models.
>Considering the limited computation power compared to today's possibilities, the results reported by Johnson are of reasonable quality.

2001年，Johnson等人发表了一个升级的宏观模型，甚至包括子层板的堆叠[22]。
这种堆叠允许使用**层间的界面模型**。
Johnson应用Allix和Ladeveze[23]的界面模型来捕捉分层损伤。
这种方法仍然为最先进的中尺度模型提供了基础。
考虑到与今天的可能性相比有限的计算能力，Johnson报告的结果是合理的质量。

>The increase of computational power permitted to apply Johnson's idea on a higher degree of detail: Meso-scale FE models capture the laminate by modeling each ply with at least one layer of elements.
>The majority of recent publications uses such a modeling approach.
>The plies are equipped with a damage-model based on continuum damage mechanics (CDM) and the cohesive zone method (CZM) according to Allix [23] is used at the interface.
>There is a vast variety of published meso-scale methods — the interface model, the ply model, element types and meshing approaches are essential characteristics in which recent models differ.
>As a meso-scale model can work with any homogenized failure condition [24,25], the choice of this condition is also an important parameter.

计算能力的提高允许将Johnson的想法应用于更高的细节：例如**中尺度的FE模型通过对每层至少有一层元素的建模来捕捉层压板。**
最近的出版物大多采用这种建模方法。
**夹层配备了基于连续损伤力学（CDM）的损伤模型**，根据Allix[23]，在界面上使用了粘着区方法（CZM）。
已发表的中尺度方法种类繁多--界面模型、层状模型、元素类型和网格划分方法是近期模型的基本特征。
由于中尺度模型可以适用于任何同质化的**失效条件**[24,25]，该条件的选择也是一个重要参数。

>In 2001, also Borg et al. published a cohesive element delamination model for composite laminates [26].
>Based on this model, the research group presented a complete meso-scale model for impact analysis in 2004 [27].
>In this model, an approach for determining the propagation direction of delamination was included.
>Published by Loikkanen el al., another meso-scale model followed in 2008 [28].
>They applied the cohesive surface method in their impact analysis model.

2001年，Borg等人也发表了一个用于复合材料层压板的粘性元素分层模型[26]。
在这个模型的基础上，该研究小组在2004年提出了一个完整的中尺度模型用于冲击分析[27]。
在这个模型中，包括了一个确定分层传播方向的方法。
由Loikkanen el al.发表的另一个中尺度模型在2008年跟进[28]。
他们在他们的冲击分析模型中应用了内聚面的方法。

>In both these works of Loikkanen and Borg, good delamination predictions are reported.
>Borg additionally identified the necessity of improved ply-damage-models.
>A correspondingly improved model was presented by Bouvet in 2010 [29] and by Gama in 2011 [30].
>Later, several adapted configurations were developed, for example by Shi in 2014 [31], Gonzalez in 2012 [5] and Tan in 2015 [3].
>Recent publications mainly provide incremental improvements.
>Better failure conditions [32], inclusion of nonlinearities and the permanent deformation [3,33-35] or the damage evolution [3,36] are proposed.
>Panettieri also identified additional relevant influence factors like the vibration behavior of the impactor [37].

在Loikkanen和Borg的这两项工作中，都报告了良好的分层预测结果。
Borg还指出了改进层状损伤模型的必要性。
Bouvet在2010年[29]和Gama在2011年[30]提出了一个相应的改进模型。
后来，一些适应性的配置被开发出来，例如，Shi在2014年[31]，Gonzalez在2012年[5]和Tan在2015年[3]。
最近的出版物主要提供了渐进式的改进。
提出了更好的**失效条件**[32]，包括**非线性和永久变形**[3,33-35]或**损伤演变**[3,36]。
Panettieri还确定了额外的相关影响因素，如冲击器的振动行为[37]。

>Good results can be achieved with these methods, even though the computation effort is high and numerical difficulties have been reported.
>Recent improvements possibly provide a better solution accuracy, but rather increase the computational effort than reducing it.
>Usually, user-defined material models are necessary for the CDM damage-models.
>Especially if permanent indentation or nonlinear shear behavior shall be included, onboard materials of commercial FE codes do not provide the required features.
>Gama implemented a suitable material model for LS-Dyna and published it under the name Mat162 [38].

用这些方法可以取得很好的结果，尽管计算工作量很大，而且有报告说有数值困难。
最近的改进可能提供了更好的求解精度，但反而增加了计算量，而不是减少了计算量。
通常情况下，用户定义的材料模型对于CDM损伤模型是必要的。
特别是当永久压痕或非线性剪切行为应包括在内时，商业有限元代码的机载材料并不能提供所需的功能。
**Gama为LS-Dyna实现了一个合适的材料模型，并以Mat162[38]的名义发布。**

>While usual meso-scale approaches capture intra-ply damage through continuum damage mechanics, Bouvet and Rivallant developed an alternative solution [29,39].
>The mesh aligns with the fiber direction, and fiber-parallel cohesive zones are put inside each ply.
>In contrast to continuum damage mechanics, cracks are captured as real singularities in the ply.
>The corresponding failure mode is called ply-splitting [29] and a type of inter-fiber failure.
>The simulation results of Bouvet show excellent agreement with experimental results on different laminates of unidirectional plies.

虽然通常的中尺度方法是通过连续损伤力学来捕捉层内损伤，但Bouvet和Rivallant开发了一个替代的解决方案[29,39]。
网格与纤维方向一致，每个层内都有与纤维平行的内聚区域。
与连续体损伤力学不同，裂缝被捕捉为层中的真实奇点。
相应的失效模式被称为层间分裂[29]，是一种纤维间的失效类型。
Bouvet的模拟结果显示与不同的单向层压板的实验结果有很好的一致性。

>Furthermore, other variants to build a meso-scale model without CDM were tried: The extended finite element method (XFEM) was considered to be suitable for lamina damage by Nian [40] and Chen [41].
>But Chen also mentioned difficulties with explicit time integration and the required computation effort.
>Other advanced methods like phase field modeling [42] or discrete elements [41] do still not provide the required maturity for application on laminated composites.

此外，还尝试了其他的变体来建立一个没有CDM的中尺度模型，Nian[40]和Chen[41]认为扩展有限元方法（XFEM）适用于板层损伤。
但Chen也提到了显式时间积分的困难和所需的计算工作量。
其他先进的方法，如相场建模[42]或离散元素[41]，**仍不能提供应用于层状复合材料所需的成熟度。**

>On the next level of detail, the prediction of inter-fiber fracture is conducted by a micromechanical model.
>Such a model needs to be coupled with a reference volume element (RVE) in a multiscale approach.
>The damage onset and the matrix damage are predicted on a micro-scale. 
>Especially for multiaxial loading, such a prediction is superior to homogenized models.
>Micromechanical failure criteria like Huang [43] or energy based matrix failure conditions [44,45] can be used. 
>Lopes et al published the first impact model on this abstraction scale in 2014 [46], in 2016 Ivančević and Smojver [47] proposed another approach.

在下一个细节层面，纤维间断裂的预测是由微观力学模型进行的。
这样的模型需要与多尺度方法中的参考体积元素（RVE）相耦合。
损伤的发生和基体损伤在微观尺度上被预测。
特别是对于多轴载荷，这样的预测比同质化的模型要好。
像Huang[43]或基于能量的基体失效条件[44,45]的微观力学失效标准可以被使用。
Lopes等人在2014年发表了这个抽象尺度上的第一个冲击模型[46]，在2016年Ivančević和Smojver[47]提出了另一种方法。

### Existing reviews

>Many researchers already have conducted reviews about impact analysis methods.
>The compendium ‘ Impact on Composite Structures' by Abrate [48] represents a review of the entire spectrum of analytical methods.
>The capabilities and the deficiencies of various spring-mass and plate models are analyzed and evaluated in this work.
>The first broadly-based review was conducted by Elder et al. in 2004 [49].
>Linear elastic fracture mechanics, macro-scale shell-models, and the damage threshold loads were tested.
>Among these, damage threshold evaluation lead to surprisingly good results.
>But the test cases were still far from possible impact use cases.
>For efficient aircraft design application, a need for further development and improved accuracy was determined.

许多研究人员已经对冲击分析方法进行了审查。
Abrate[48]编写的 "复合结构的冲击 "汇编代表了对整个分析方法的审查。
在这项工作中，分析和评估了各种弹簧-质量和板材模型的能力和不足之处。
第一个广泛的审查是由Elder等人在2004年进行的[49]。
对线性弹性断裂力学、宏观尺度的壳模型和损伤阈值载荷进行了测试。
其中，损伤阈值评估导致了令人惊讶的好结果。
**但这些测试案例仍然与可能的冲击使用案例相去甚远**。
**对于有效的飞机设计应用，需要进一步发展和提高精度**。

>Also about recent high-fidelity models, reviews have been published.
>A comparison of the predictive capabilities with different
>failure criteria was conducted by Liu et al. [32].
>Their model is based on stacked-solid approach with cohesive elements. 
>According to their results, the Puck criterion leads to the most reliable results.
>Force history, energy dissipation, and damage initiation forces were plausibly predicted.
>Other criteria also lead to proper results.
>In consequence, it is appropriate to trade off between accuracy and computation effort for particular applications.

另外，关于最近的高保真模型，已经发表了评论。
Liu等人对不同失效标准的预测能力进行了比较。
Liu等人[32]进行了不同失效标准的预测能力比较。
他们的模型是基于具有粘性元素的堆积固体方法。
根据他们的结果，**Puck准则**导致了最可靠的结果。
力的历史、能量耗散和破坏开始的力量都被合理地预测了。
其他标准也导致了适当的结果。
因此，对于特定的应用，在准确性和计算工作量之间进行权衡是合适的。

>In 2015, Lopes et al. conducted another benchmark about impact simulation methods [34].
>Four different meso-scale modeling strategies with varying mesh structures and cohesive zone models were presented and compared.
>Aligned meshing improved the prediction of the intralaminar failure and the delamination.
>Cohesive surfaces permitted to include the friction behavior of two delaminated plies and also lead to improvements in the overall results.

2015年，**Lopes等人进行了另一个关于冲击模拟方法的基准测试**[34]。
他们提出了四种不同的中尺度建模策略，并对不同的网格结构和粘着区模型进行了比较。
对齐的网格结构提高了对层内破坏和分层的预测能力。
粘着面允许包括两个分层的摩擦行为，也导致了整体结果的改善。

>In addition to that, Jousset published a comparison of two different possibilities to employ a constitutive law in a cohesive zone [50].
>A standard bi-linear traction separation law was compared to a pressure dependent elasto-plastic damage-model.
>An elastoplastic model showed a better behavior if the interface material showed significant plastic yield.
>May's evaluation of cohesive laws [51] included strain rate effects.
>He provided an overview of the required enhancements and identified strain rate effects as crucial only beyond LVI and quasistatic events.
>Abisset et al. proved in their work the equivalence of damage morphology between quasi-static indentation and LVI [52].
>On the numerical side, the influence of cohesive parameters on the impact response was analyzed by Panettieri et al. [53].

除此之外，Jousset还发表了在粘着区采用构成法的两种不同可能性的比较[50]。
一个标准的**双线性牵引分离法**与一个**压力相关的弹塑性损伤模型**进行了比较。
如果界面材料表现出明显的塑性屈服，弹塑性模型表现出更好的行为。
**May对内聚力定律的评估[51]包括了应变率效应**。
他提供了一个所需增强的概述，并确定应变率效应仅在LVI和准静态事件之外才是关键。
Abisset等人在他们的工作中证明了准静态压痕和LVI之间损伤形态的等同性[52]。
在数值方面，Panettieri等人分析了内聚力参数对冲击响应的影响[53]。

>The state-of-the-art modeling approach with a meso-scale model is also used beyond the analysis of LVI [3,32,34,54].
>Corresponding models for high-velocity impact were proposed by Pernas-Sanchez et al. [55] or by Heimbs et al. [56].
>A comparable approach is also applied for crushing analysis [57] and for general damage modeling in composite structures [58].

具有中尺度模型的最先进的建模方法也被用于LVI的分析之外[3,32,34,54]。
Pernas-Sanchez等人[55]或Heimbs等人[56]提出了对应的高速冲击模型。
一个类似的方法也被应用于破碎分析[57]和复合材料结构中的一般损伤建模[58]。

### Prediction of damage visibility

>In addition to the damage itself, the damage visibility is of significant interest for the numerical prediction.
>The visibility determines whether a damage will be discovered and repaired.
>In aircraft application commonly a limit value of permanent indentation at the impact spot is applied to define the visibility limit.
>Additionally also the fiber crack length on the impact side can be taken into account to assess the visibility.
>The fiber crack length is predicted by nearly all finite element models accomplishing damage analysis.
>In contrast to that, additional implementations are necessary to capture the permanent indentation model.

除了损害本身，损害的能见度对数值预测也有重要的意义。
**能见度决定了损伤是否会被发现和修复**。
在飞机应用中，**通常采用撞击点的永久压痕的极限值来定义可见性极限**。
**此外，在评估可见性时，也可以考虑到冲击侧的纤维裂纹长度。**
几乎所有完成损伤分析的有限元模型都**预测了纤维裂纹长度。**
与此相反，额外的实现对于捕捉永久压痕模型是必要的。

>The physical causes of permanent indentation are resin plasticity and the impeded crack closure in the unloading phase [59].
>When the crack closes, resin debris can prevent a crack from fully closing.
>This phenomenon affects both tensile and shear cracks.
>There are several possibilities reported in the literature to capture it.

**永久性压痕的物理原因是树脂的可塑性和在卸载阶段阻碍了裂缝的闭合**[59]。
**当裂缝闭合时，树脂碎屑会阻止裂缝完全闭合。**
这种现象对拉伸和剪切裂纹都有影响。
文献中报道了几种可能性来捕捉它。

>The most simple prediction is an empirical description by an analytical formula [48].
>Using the contact law of Hertz [60] and a damage threshold permits to compute a value for the permanent surface indentation.
>The evaluation of such a formula is possible within the postprocessing of most impact analysis methods.
>For example, Li et al. [61] proposed a corresponding method: based on a finite element model the permanent indentation is captured by an analytical law relying on the Hertzian contact.

**最简单的预测是通过分析公式的经验描述**[48]。
**使用Hertz[60]的接触定律和损伤阈值可以计算出永久性表面压痕的数值**。
在大多数冲击分析方法的后处理中都可以评估这样一个公式。
例如，Li等人[61]提出了一个相应的方法：基于有限元模型，永久压痕被一个依赖于赫兹接触的分析法所捕获。

>Capturing the permanent indentation in a finite element model requires an adaption of the constitutive law.
>An appropriate model of the unloading phase is essential.
>The stress has to reach zero before the strain reaches its zero-point.
>A simple bilinear degradation law does not serve this purpose as the unloading always goes along a secant to the origin.
>In 2011, Falzon and Apruzzese proposed a method to capture the permanent deformation based on the non-linear shear behavior [58,62].
>This method was also applied in the advanced impact simulation model of Tan and Falzon [3].
>Fanteria et al. [63] confirmed that the permanent indentation predicted by that method is qualitatively analogous to the indentation in experiments.
>In a sensitivity analysis, they pointed out that an accurate knowledge about the non-linear shear behavior is significant for quantitative prediction of the indentation values.

**在有限元模型中捕捉永久压痕需要对本构方程进行调整**。
**卸载阶段的适当模型是必不可少的**。
**应力必须在应变达到零点之前达到零**。
简单的双线性退化规律不能满足这一目的，因为卸载总是沿着对原点的正切线进行。
2011年，Falzon和Apruzzese提出了一种**基于非线性剪切行为的捕捉永久变形的方法**[58,62]。
该方法也被应用于Tan和Falzon[3]的高级冲击模拟模型。
Fanteria等人[63]证实，该方法所预测的永久压痕与实验中的压痕在质量上是类似的。
在敏感性分析中，他们指出，对非线性剪切行为的准确了解对压痕值的定量预测很重要。

>Another approach was developed by Bouvet et al. [59].
>This approach is based on the previously mentioned ply-splitting model with intra-ply cohesive zones.
>The constitutive law of the cohesive elements capturing matrix damage is adapted.
>After tensile or shear damage occurred, a stress of zero is reached before the strain reaches zero.
>The element responds with compression stress if the strain becomes smaller than this predefined value.
>This law shall directly describe the effect of resin debris blocking the crack.

**另一种方法是由Bouvet等人开发的[59]。**
**这种方法是基于前面提到的带有层内粘连区的层间裂缝模型**。
**捕捉基体损伤的粘着元素的构成法被调整**。
在发生拉伸或剪切损伤后，在应变达到零之前，应力达到零。
如果应变变得小于这个预定值，该元素就会以压缩应力作出反应。
这个规律应直接描述树脂碎片阻挡裂缝的效果。

>Lopes et al. suggest another alternative that works with a cohesive surface model [34].
>They used the static friction of opposing crack planes prevents the delamination from closing.
>That way, also a permanent deformation is described.

**Lopes等人提出了另一个替代方案，它与粘性表面模型一起工作**[34]。
他们用对立的裂缝平面的静态摩擦力来阻止分层的闭合。
这样一来，也就描述了一个永久变形。

>Apart from the visibility, the permanent indentation has also a significant influence on the energy absorption as Caprino et al. showed in their study [64] and confirmed by Fanteria et al. [63].
>After the impact, residual stresses remain in the laminate.
>This elastic energy also contributes to the total energy absorption.
>Accordingly, models without a permanent indentation model underestimate this value.
>Although the prediction of permanent indentation is not part of the benchmark in this study, it is important to mention that its prediction is also a crucial part of LVI analysis as it determines the visibility.

**除了能见度，永久压痕对能量吸收也有很大的影响**，Caprino等人在他们的研究中表明[64]，并由Fanteria等人[63]证实。
冲击过后，残余应力仍留在层压板中。
这种弹性能量也对总的能量吸收有贡献。
相应地，没有永久压痕模型的模型低估了这个数值。
尽管永久压痕的预测不是本研究中基准的一部分，但必须提及的是，它的预测也是LVI分析的一个关键部分，因为它决定了可见性。

### Impact analysis on the structural level

>Sufficiently accurate modeling strategies are available, the current challenge is the application of impact analysis on the structural level.
>While the predictive capabilities seem satisfactory, the corresponding computation effort is already very high for small coupon specimens.
>For coupon simulations of CAI impacts, Tan reports a computation time of 19 h on 32 CPUs [3], Lopes even 48 h on 40 CPUs, as a very fine mesh was applied.
>These numbers show that a blunt transfer of the same method to structural level would result in inefficiently high computation effort.
>For some methods, also the modeling effort can severely increase.

足够精确的建模策略已经存在，目前的挑战是在结构层面上应用冲击分析。
虽然预测能力似乎令人满意，但相应的计算工作对于小型券片试样来说已经非常高了。
对于CAI冲击的试样模拟，Tan报告在32个CPU上的计算时间为19小时[3]，Lopes甚至在40个CPU上的计算时间为48小时，因为采用了非常细的网格。
这些数字表明，将同样的方法钝化到结构层面会导致低效率的高计算量。
对于某些方法，建模的工作量也会严重增加。

>An excellent example for a structural application of a high-fidelity impact analysis was published by Schwab and Pettermann in 2016 [65].
>The definition of a damage-prone area permits to work with differently meshed zones.
>Riccio proposes in several publications a comparable approach [66,67].
>He also applies a local analysis approach with a damage-prone area and uses it already on the coupon level in order to reduce the computational costs.
>Both, Riccio and Schwab achieved good results with this local impact damage analysis.
>Also, Riccio presented the application of a meso-scale model on a substructural level [68].
>Johnson works directly with a cut-out section of the actual structure [69].
>Low-fidelity methods with a layered-shell mesh can directly be applied on the structural level, as the number of DoF is significantly lower [20].

Schwab和Pettermann在2016年发表了一个关于高保真冲击分析的结构应用的优秀案例[65]。
损伤易发区的定义允许在不同的网格区域工作。
Riccio在一些出版物中提出了一种类似的方法[66,67]。
他还应用了一个具有易损区的局部分析方法，并在券面上使用，以减少计算成本。
Riccio和Schwab都通过这种局部冲击损伤分析取得了良好的效果。
此外，Riccio还介绍了中尺度模型在子结构层面的应用[68]。
Johnson直接用实际结构的切面进行工作[69]。
采用分层壳网的低保真方法可以直接应用于结构层面，因为自由度的数量明显减少[20]。

## Applied damage prediction methods

### Delamination threshold forces

### Cohesive zone method(CZM)

### Continuum damage mechnics(CDM)

## Implemented impact models for comparison

### Spring mass model

### Plate model

### Layered-shell model

### Stacked shell model

### Stacked-solid model

### Ply-splitting model

## Benchmark

### Impact test cases

### Analysis Results

### Conclusion of the coupon benchmark
