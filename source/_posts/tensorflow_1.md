---
title: TensorFlow入门：简介
date: 2017-07-14
categories: 深度学习
tags: [深度学习,神经网络,TensorFlow]
---
TensorFlow 是一个用于人工智能的开源神器

## TensorFlow是什么？
TensorFlow™ 是一个采用数据流图（data flow graphs），用于数值计算的开源软件库。节点（Nodes）在图中表示数学操作，图中的线（edges）则表示在节点间相互联系的多维数据数组，即张量（tensor）。它灵活的架构让你可以在多种平台上展开计算，例如台式计算机中的一个或多个CPU（或GPU），服务器，移动设备等等。TensorFlow 最初由Google大脑小组（隶属于Google机器智能研究机构）的研究员和工程师们开发出来，用于机器学习和深度神经网络方面的研究，但这个系统的通用性使其也可广泛用于其他计算领域。
![TensorFlow](1.gif)

## 什么是数据流图（Data Flow Graph）?
数据流图用“结点”（nodes）和“线”(edges)的有向图来描述数学计算。“节点” 一般用来表示施加的数学操作，但也可以表示数据输入（feed in）的起点/输出（push out）的终点，或者是读取/写入持久变量（persistent variable）的终点。“线”表示“节点”之间的输入/输出关系。这些数据“线”可以输运“size可动态调整”的多维数据数组，即“张量”（tensor）。张量从图中流过的直观图像是这个工具取名为“Tensorflow”的原因。一旦输入端的所有张量准备好，节点将被分配到各种计算设备完成异步并行地执行运算。

## TensorFlow的特征
+ 高度的灵活性
+ 真正的可移植性（Portability）
+ 将科研和产品联系在一起
+ 自动求微分
+ 多语言支持
+ 性能最优化
