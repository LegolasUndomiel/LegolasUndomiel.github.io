---
title: 2012-Bouvet-Low velocity impact
date: 2022-03-16 10:59:53
tags:
---

## Abstract

>This paper deals with impact damage and permanent indentation modeling.
>A numerical model has been elaborated in order to simulate the different impact damage types developing during low velocity/low energy impact.
>The three current damage types: matrix cracking, fiber failure and delamination, are simulated.
>Inter-laminar damage, i.e. interface delamination, is conventionally simulated using interface elements based on fracture mechanics.
>Intra-laminar damage, i.e. matrix cracks, is simulated using interface elements based on failure criterion.
>Fiber failure is simulated using degradation in the volume elements.
>The originality of this model is to simulate permanent indentation after impact with a ‘‘plastic-like’’ model introduced in the matrix cracking elements.
>This model type is based on experimental observations showing matrix cracking debris which block crack closure.
>Lastly, experimental validation is performed, which demonstrates the model’s satisfactory relevance in simulating impact damage.
>This acceptable match between experiment and modeling confirms the interest of the novel approach proposed in this paper to describe the physics behind permanent indentation.

本文讨论了冲击损伤和永久压痕模型。
为了模拟在低速/低能量冲击过程中形成的不同的冲击损伤类型，已经详细制定了一个数值模型。
模拟了目前的三种损伤类型：基体开裂、纤维失效和分层。
**层间损伤，即界面分层，传统上使用基于断裂力学的界面元素进行模拟。**
**层内损伤，即基体裂缝，使用基于失效准则的界面元素进行模拟。**
**纤维破坏是使用体积元素的退化来模拟的。**
这个模型的独创性在于用矩阵裂纹元素中引入的“类塑料”模型模拟冲击后的永久压痕。
这种模型类型是基于实验观察，显示了阻碍裂缝闭合的基体开裂碎片。
最后，进行了实验验证，证明了该模型在模拟冲击损伤方面具有令人满意的相关性。
实验和建模之间的这种可接受的匹配证实了本文提出的描述永久压痕背后的物理学的新方法的重要性。

## Introduction

## Modeling principle
>A low velocity/low energy impact on a composite laminate with UD reinforcement induces three types of damage: matrix cracks, fiber failure and delamination.

低速/低能量冲击带有UD加固的复合材料层压板会引起三种类型的损伤：基体裂纹、纤维失效和分层。

>Conventionally, the first damage to appear is matrix cracking.
>When this damage increases, delamination quickly occurs.
>Interaction between these two damage phenomena is clearly visiblev during impact tests.
>This interaction is crucial to explain the very original morphology of the delaminated interfaces through the thickness of the plate.
>Chang and Chang illustrate this interaction [11] in Fig. 3c which schematically shows the two types of delamination formation:
>
>The delamination induced by inner shear cracks which generates a substantial delamination along the bottom interface and a small confined delamination along the upper interface of the cracked plies.
>The delamination induced by a surface bending crack, which generates a delamination along the first interface of the cracked ply.

传统上，**首先出现的损伤是基体开裂**。
**当这种损伤增加时，分层迅速发生。**
在冲击试验中，这两种损伤现象之间的相互作用是显而易见的。
这种相互作用对于解释通过板材厚度的分层界面的非常原始的形态至关重要。
Chang和Chang在图3c中说明了这种相互作用[11]，该图示意性地显示了两种类型的分层形成。

由**内部剪切裂纹**引起的分层，沿底部界面产生大量的分层，沿裂纹层的上部界面产生小的封闭分层。
由**表面弯曲裂纹**引起的分层，沿开裂层的第一界面产生分层。

>Consequently, the key point for an impact model is the interaction between intra-laminar damage, namely matrix cracks and fiber failure, and inter-laminar damage, namely delamination.
>Some models in the literature (e.g. [8–10,17,26]) take this interaction into account using explicit relations between the damage variables of matrix cracking in the ply and the damage variables of delamination between plies.
>Another way to model this interaction is to allow for the discontinuity created by matrix cracks, in order to naturally account for this interaction [8,27].
>Indeed, this discontinuity seems essential for the formation of the impact damage [28] and should be modeled to correctly simulate this damage morphology.
>Consequently, the plies mesh must respect the material orthotropy in order to account for the discontinuity aspect of the matrix cracks in the fiber direction.
>Then, in the proposed model, each ply is meshed separately using little longitudinal strips with one volume element in the ply thickness (Fig. 4).

因此，**冲击模型的关键点是层内损伤，即基体裂纹和纤维失效，与层间损伤，即分层之间的相互作用**。
文献中的一些模型（如[8-10,17,26]）使用**层内基体裂纹的损伤变量和层间分层的损伤变量之间的明确关系**来考虑这种相互作用。
另一种建立这种相互作用模型的方法是**允许基体裂纹产生的不连续性**，以便自然地考虑这种相互作用[8,27]。
事实上，**这种不连续性似乎对冲击损伤的形成至关重要[28]**，应该对其进行建模以正确模拟这种损伤形态。
因此，层网必须尊重材料的正交性，以说明纤维方向上的基体裂纹的不连续性方面。
然后，在所提出的模型中，每个夹层用小的纵向条带单独网格化，在夹层厚度上有一个体积元素（图4）。

### Matrix cracking modeling

>Afterwards, these little strips are connected together with zerothickness interface elements normal to the transverse direction.
>These interface elements can account for matrix cracks in the thickness of the ply.
>Nevertheless, this type of mesh presents some drawbacks:

之后，这些小条状物与横向的零厚度界面元素连接在一起。
这些界面元素可以说明层压板厚度上的矩阵裂缝。
然而，这种类型的网格有一些缺点：

>- This mesh is complicated by uniform size in the impact zone.
>Nevertheless, it is possible to simulate an impact on a real structure using a multi-scale approach: the model described above for the area concerned with impact damage, and a conventional FE model for the remaining structure [29].

这种网格因冲击区的均匀尺寸而变得复杂。
尽管如此，还是有可能使用多尺度的方法来模拟对真实结构的冲击：对与冲击损伤有关的区域使用上述模型，对其余结构使用传统的FE模型[29]。

>- This mesh can only simulate cracks occurring through the entire thickness of the ply and is not able to simulate small, diffusive matrix cracks.
>This means the propagation of matrix cracks within the ply thickness is assumed to be instantaneous.
>Thus, if the ply thickness is not too great,the propagation of a matrix crack in the thickness takes place very quickly and its effect on the creation of the impact damage should remain local.

这种网格**只能模拟通过整个层板厚度发生的裂缝，无法模拟小的、扩散性的基体裂缝**。
这意味着**基体裂缝在层板厚度内的传播被假定为是瞬时的**。
因此，如果夹层厚度不是太大，基体裂纹在厚度内的传播会很快发生，它对冲击破坏的产生的影响应该是局部的。

>- This mesh can only simulate cracks normal to interfaces.
>However, matrix cracks due to out-of-plane shear stress (stz), are globally inclined at 45.
>This hypothesis avoids the use of an overly complex mesh, and seems reasonable if the ply thickness is small compared to the laminate thickness.

这种网格只能模拟界面上的法线裂缝。
然而，由于平面外剪应力（stz）导致的基体裂纹，在全球范围内倾斜45。
这一假设避免了使用过于复杂的网格，如果层压板厚度与层压板厚度相比较小的话，这一假设似乎是合理的。

>- The mesh size imposes the maximum density of matrix cracks in the transverse direction of the ply.
>This drawback could seem very significant but the presence of one matrix crack, i.e. of a broken interface, should unload the neighboring interfaces in the transverse direction and prevent their breaking.
>Indeed, the matrix cracks, taken into account in this model, are only the largest ones, i.e. those running through the entire ply thickness, and not the little, diffuse matrix cracks.
>This means that the model does not take into account the network of little matrix cracks because the effect of these diffuse matrix cracks seems small compared to those running through the entire thickness.

网格大小规定了层压板横向上的基体裂纹的最大密度。
这个缺点似乎非常重要，但是一个基体裂纹的存在，即一个断裂的界面，应该使横向上的相邻界面卸下负荷，防止它们断裂。
事实上，在这个模型中考虑到的矩阵裂纹只是最大的裂纹，即贯穿整个层板厚度的裂纹，而不是小的、分散的矩阵裂纹。
这意味着该模型没有考虑到小的矩阵裂纹网络，因为与贯穿整个厚度的裂纹相比，这些弥散的矩阵裂纹的影响似乎很小。

>Another consequence of this imposed maximum density of matrix cracks is the choice of the failure criterion and energy dissipated by this phenomenon.
>It would be interesting to use fracture mechanics, in addition to interface elements, to simulate the critical energy release rate [30].
>But the mesh density is imposed a priori and induces the maximum energy possible to dissipate, unless the mesh is fine enough to simulate each crack.
>As it is not possible to simulate each matrix crack (Fig. 2a), the proposed model has been chosen without energy dissipation.

这种强加的矩阵裂纹最大密度的另一个后果是**失效标准的选择和这种现象所耗散的能量**。
除了界面元素外，使用断裂力学来模拟临界能量释放率是很有趣的[30]。
但是网格密度是先验的，并诱导出可能耗散的最大能量，除非网格细到足以模拟每个裂缝。
由于不可能模拟每条基体裂纹（图2a），**所提出的模型被选择为没有能量耗散**。

>Then the model ignores the energy dissipated by matrix cracking, even if a part of this energy should be included in the energy dissipated by delamination.
>Indeed, the DCB (Double Cantilever Beam) test, which is used to evaluate the critical energy release rate for delamination, is a overall test.
>In practical terms, the energy dissipated during the test which is experimentally evaluated, is the sum of all damage types [31,32].
>In particular, the energy dissipated by the matrix cracks, accompanying the delamination, is taken into account.
>Nevertheless, the consequences of this non-dissipative model should be evaluated with other experimental tests.
>Another solution would be to use cohesive crack modeling to allow multiple matrix cracks per element, as proposed by Raimondo et al. [33].

那么该模型就**忽略了基体裂纹所耗散的能量**，即使该能量的一部分应该包括在分层所耗散的能量中。
事实上，DCB（双悬臂梁）试验，用来评估分层的临界能量释放率，是一个整体试验。
在实践中，实验评估的测试期间的能量耗散，是所有破坏类型的总和[31,32]。
特别是，伴随着分层的基体裂缝耗散的能量被考虑在内。
尽管如此，这种非耗散性模型的后果应该用其他实验测试来评估。
**另一个解决方案是使用内聚裂纹模型，允许每个元素有多个基体裂纹，正如Raimondo等人[33]所提议的。**

>In the proposed case, the interface degradation is abrupt: if the material is safe, the stiffness of these matrix cracking interfaces is considered to be very high and this stiffness is set to zero if matrix cracks exist.
>Of course, this abrupt degradation can induce shock issue during numerical simulation and additional damping should be added [22].
>The energy dissipated by this viscosity damping should remain low [34], typically less than 2% of the total energy.

**在提议的情况下，界面退化是突然的：如果材料是安全的，这些矩阵裂缝界面的刚度被认为是非常高的，如果存在矩阵裂缝，这个刚度被设置为零。**
**当然，这种突然的退化会在数值模拟过程中诱发冲击问题，应该增加额外的阻尼[22]。**
这种粘性阻尼所耗散的能量应该保持在较低水平[34]，通常小于总能量的2%。

>The failure is driven by a standard criterion similar to Hashin’s criterion [35,36], calculated in the neighboring volume elements:
>where rt is the transverse stress, slt and stz the shear stresses in the (lt) and (tz) planes, < >+ the positive value, rft the transverse failure stress and sf lt the shear failure stress of the ply.
>This conventional quadratic criterion [35,36] is written with stresses at each Gauss point of the two neighboring volume elements and the interface is broken when the criterion is reached at one of these points (for more details, see [24]).
>This is an original point of the proposed model and can be considered to be an average stress over a distance which depends on the mesh size.
>This mesh sensitivity will have to be studied further; this work is currently in progress.

**失败是由类似于Hashin准则的标准准则驱动的[35,36]，在相邻的体积元素中计算。**
其中rt是横向应力，slt和stz是(lt)和(tz)平面上的剪切应力，< >+是正值，rft是横向破坏应力，sf lt是层压的剪切破坏应力。
这个传统的二次准则[35,36]是以两个相邻体积元素的每个高斯点的应力来写的，当在这些点之一达到准则时，界面就会被打破（更多细节，见[24]）。
这是所提出的模型的一个原始点，可以认为是一个取决于网格大小的距离上的平均应力。
这种网格敏感性将不得不进一步研究；这项工作目前正在进行中。

>Hereafter, these matrix cracking interface elements are used to simulate permanent indentation.
>Indeed, part of the permanent indentation seems to be impact debris in 45 cracks through the ply thickness (Fig. 2) [12].
>This phenomenon has been taken into account in the present model using an original ‘‘plastic-like’’ model behavior in the matrix cracking elements in order to limit their closure after failure under tension (rt) and out-of-plane shear (stz) (Fig. 5).
>The formulation of the law after crack initiation is given below:

此后，这些矩阵裂纹界面元素被用来模拟永久压痕。
事实上，部分永久压痕似乎是通过层厚的45条裂缝中的冲击碎片（图2）[12]。
这一现象在本模型中已经被考虑到了，在基体裂纹元素中使用了原始的''类塑性''模型行为，以限制其在张力（rt）和平面外剪切力（stz）下失效后的闭合（图5）。
下面给出了裂缝发生后的法则表述。

>where kt and ktz are the stiffness values of debris, et and ctz are the dimensionless displacements of the interface displacements, and 0 t and c0 tz the dimensionless sizes (Fig. 5) of these debris respectively in the normal direction and in shear:
>where w is the width of the element and u0 and v0 are the sizes of the debris respectively in the normal and transverse direction.

其中kt和ktz是碎片的刚度值，et和ctz是界面位移的无量纲位移，0 t和c0 tz分别是这些碎片在法向和剪切中的无量纲尺寸（图5）。
其中w是元素的宽度，u0和v0分别是碎片在法向和横向的尺寸。

>Then, when a matrix crack exists, its closure is prevented if its dimensionless displacement et (ctz) is below a critical size 0 t (c0 tz) corresponding to the debris size.
>This critical debris size can be compared to the critical indentation acr (Eq. (1)) proposed by Karakuzu et al. [21].

那么，当矩阵裂缝存在时，如果其无量纲位移et（ctz）低于与碎片尺寸相对应的临界尺寸0 t（c0 tz），则其闭合被阻止。
这个临界碎片尺寸可以与Karakuzu等人[21]提出的临界压痕acr（公式（1））相比。

>If the crack is assumed to be 45 in the (tz) plane these two stiffness values and debris sizes are equivalent and are assumed to be equal:

如果假设裂纹在(tz)平面内为45，这两个刚度值和碎片尺寸是等效的，并被认为是相等的。

>Consequently, only two material parameters are necessary to take into account the phenomenon of permanent indentation.
>These two parameters are difficult to correlate with material parameters measured in conventional tests and are directly determined using the impact test.
>Therefore, this evaluation process limits the predictive character of this model, and in particular for the part linked to permanent indentation.
>Other works are in progress to evaluate these parameters using simpler experimental studies.
>It can be observed that these two parameters are the only ones in this model which are directly determined during the impact test: all other values are obtained from conventional experimental tests described in the literature [31,32,37,38,41].

因此，只有两个材料参数需要考虑到永久压痕现象。
这两个参数很难与传统测试中测量的材料参数相关联，而是直接使用冲击试验来确定。
因此，这个评估过程限制了这个模型的预测性，特别是与永久压痕有关的部分。
其他工作正在进行中，以使用更简单的实验研究来评估这些参数。
可以看到，这两个参数是这个模型中唯一在冲击试验中直接确定的参数：**所有其他的值都是从文献[31,32,37,38,41]中描述的常规实验测试中得到的。**

>This no-closure model integrated into the interface elements of matrix cracking makes it possible to obtain a realistic deformed shape of the plate, not only during impact but also after impact, as well as a permanent indentation (Fig. 14).

这种无封闭模型集成到基体开裂的界面元素中，使得有可能获得真实的板材变形形状，不仅在冲击过程中，而且在冲击后，以及永久压痕（图14）。

### Fiber failure modeling

>For the fiber failures observed after impact (Fig. 2), there is no evidence of distributed fiber damage.
>Moreover, due to the high critical energy release rate of fiber failure [38], it is necessary to dissipate this energy in the model.
>Additional interface elements could be used but would result in very complex meshing.
>Therefore, to avoid the use of such interfaces, fiber failure is taken into account using conventional continuum damage mechanics with original formulation to produce a constant energy release rate per unit area.
>This approach can be compared to methods based on characteristic element length, which makes mesh-size independent modeling possible [15,35,39,40].

对于冲击后观察到的纤维故障（图2），没有证据表明有**分布式纤维损伤**。
**此外，由于纤维失效的临界能量释放率很高[38]，有必要在模型中消散这些能量。**
可以使用额外的界面元素，但会导致非常复杂的网格划分。
因此，为了避免使用这种界面，使用传统的**连续体损伤力学**的原始配方来考虑纤维破坏，以产生单位面积的恒定能量释放率。
这种方法可以与基于特征元素长度的方法相比较，这使得网格大小无关的建模成为可能[15,35,39,40]。

>Therefore, in order to simulate the critical energy release rate due to fiber failure per unit area of crack, the dissipated energy of a volume element should be:
>where el (rl) is the longitudinal stress (strain), V (S) the volume (section) of the element, e1 is the strain of total degradation of the fiber stiffness (Fig. 6) and Gf I the energy release rate in opening mode in the direction of the fibers.
>In this case, the law is written only in opening mode I (Fig. 6), but could be generalized with other fracture modes.

因此，为了模拟每单位面积裂缝中的纤维失效所导致的临界能量释放率，体积元素的耗散能量应该是。
其中el（rl）是纵向应力（应变），V（S）是元素的体积（截面），e1是纤维刚度总退化的应变（图6），Gf I是纤维方向上的开放模式的能量释放率。
在这种情况下，该定律只写在开放模式I中（图6），但也可以用其他断裂模式进行概括。

>Afterwards, the stiffness in fibers is degraded using a damage variable df:
>where Hll, Hlt and Hlz are the stiffness values in the longitudinal direction. And this damage variable is conventionally calculated according to the longitudinal strain in order to obtain a linear decrease of the longitudinal stress (Fig. 6) [15]:
>where e1 is calculated using Eq. (6) and e0 is the strain of damage initiation.

之后，纤维中的刚度使用损伤变量df进行降解。
其中Hll、Hlt和Hlz是纵向方向的刚度值。而这个损伤变量按惯例是根据纵向应变来计算的，以获得纵向应力的线性下降（图6）[15]。
其中e1是用公式（6）计算的，e0是损伤开始时的应变。

>An originality of this fiber failure approach is to initiate the damage when the maximum of the longitudinal strains calculated at the element nodes reaches the fiber failure strain f l .
>The use of extrapolated strains at element nodes, rather than direct strain values at integration points, makes it easier to take into account the bending behavior of each ply with only one finite volume element in the thickness.
>Nevertheless, this condition prevents the use of reduced integration elements and involves the use of eight Gauss points elements.
>Then, the e0 parameter is common to the eight Gauss points of each element and is evaluated using the longitudinal strains   alculated at the element nodes.
>The e1 and df parameters are also chosen common to the eight Gauss points in order to solve the Eq. (6) only one time for each element.

**这种纤维破坏方法的一个独到之处是，当元素节点上计算的纵向应变的最大值达到纤维破坏应变f l时，就开始破坏。**
**使用元素节点上的外推应变，而不是积分点上的直接应变值，使得在厚度上只用一个有限体积元素就能更容易考虑到每个层的弯曲行为。**
尽管如此，这个条件阻止了减少积分元素的使用，涉及到八个高斯点元素的使用。
然后，e0参数是每个元素的八个高斯点所共有的，并使用元素节点上计算的纵向应变来评估。
e1和df参数也被选为八个高斯点的共同参数，以便在每个元素上只求解一次公式。(6)对每个元素只求解一次。

### Delamination modeling

>After the different plies are meshed with volume elements and matrix crack interface elements (Fig. 4), two consecutive plies are joined using zero-thickness interface elements (Fig. 7).

在用体积元素和矩阵裂缝界面元素对不同的层进行网格化处理后（图4），用零厚度的界面元素将两个连续的层连接起来（图7）。

>These delamination interface elements are conventionally softening interfaces [30,42] of zero thickness, driven by fracture mechanics.
>They are written in mixed fracture mode (modes I, II, III) to simulate the energy dissipated by delamination.
>Moreover, the shearing (II) and tearing (III) fracture modes are combined and in the following, the term of mode II will be abusively used to name fracture modes II and III.
>Then, an equivalent relative displacement jump is written in order to simulate a linear coupling law between the fracture modes:

这些脱层界面元素是传统的零厚度软化界面[30,42]，由**断裂力学驱动。**
它们以混合断裂模式（模式I、II、III）编写，以模拟分层所耗散的能量。
此外，剪切（II）和撕裂（III）断裂模式被结合起来，在下文中，模式II的术语将被滥用于命名断裂模式II和III。
然后，为了模拟断裂模式之间的线性耦合规律，写出了一个等效的相对位移跃迁。

>This model adopted for delamination is often used in the literature [8,28] although this expression (Eq. (9)) is original.
>The definition of this equivalent relative displacement jump enables us to automatically compare all the possible mode ratios and how much energy should still be available to dissipate until total failure occurs.
>Indeed, during complex loading, with large variation in the mode ratio, it is not very easy to evaluate this remaining energy to be dissipated using conventional formulation[30,41].

尽管这个表达式（公式（9））是原创的，但文献[8,28]中经常使用这个用于脱层的模型。
这个等效相对位移跃迁的定义使我们能够自动比较所有可能的模式比率，以及在完全破坏发生之前应该还有多少能量可以消散。
事实上，在复杂的加载过程中，由于模态比有很大的变化，用传统的公式来评估这个剩余能量的耗散不是很容易[30,41]。

## Experimental validations

## Conclusion
