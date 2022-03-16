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
另一个解决方案是使用内聚裂纹模型，允许每个元素有多个基体裂纹，正如Raimondo等人[33]所提议的。

### Fiber failure modeling

### Delamination modeling

## Experimental validations

## Conclusion
