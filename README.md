# Unity Shader入门精要

## 基础篇

### 第二章 渲染流水线

- 概念流水线

	- 应用阶段-几何阶段-光栅化阶段

- CPU与GPU之间的通信

	- 把数据加载到显存中
	- 设置渲染状态
	- 调用DrawCall

- GPU流水线

	- 顶点数据
	- 顶点着色器

		- 顶点着色器是流水线的第一个阶段，需要完成坐标变换和逐顶点光照
		- 坐标变换：就是将顶点坐标转换到齐次裁剪坐标系下

	- 曲面细分着色器
	- 几何着色器
	- 裁剪
	- 屏幕映射

		- 屏幕映射将坐标映射到屏幕坐标系下

	- 三角形设置

		- 计算三角网格表示的数据

	- 三角形遍历

		- 三角形遍历 (Triangle Traversal) 阶段将会检查每个像素是否被 一 个三角网格所覆盖。如果被覆盖的话，就会生成一个 片元 (fragment) 。而这样一个找到哪些像素被三角网格覆盖的过程就是三角形遍历，这个阶段也被称为 扫描变换 (Scan Conversion) 。

	- 片元着色器

		- 片元着色器 (Fragment Shader) 是另 一 个非常重要的可编程着色器阶段。在 DirectX 中，片元着色器被称为 像素着色器 (Pixel Shader) , 但片元着色器是 一 个更合适的名字，因为此时的片元并不是一个真正意义上的像素。

	- 逐片元操作

		- 片元通过模板测试、深度测试、混合，输出到颜色缓冲区中

	- 屏幕图像

- 什么是DrawCall

	- 由于大部分情况下，GPU执行的速度很快，实际上在Draw Call中拖后腿的反而是CPU
	- 当Draw Call多的时候，每次Draw Call都需要让CPU来准备数据，因此会耗费很多时间
	- 通过批处理、避免使用大量小网格、避免使用过多材质，可以有效的减少Draw Call

### 第三章 Unity Shader基础

- Unity Shader概述
- Shader Lab

	- Shader Lab是unity提供的一个更高层级的渲染抽象层
	- ShaderLab定义了一个材质所需要的所有东西，而不仅仅是着色器代码
	- Shader "ShaderName " {
Properties {
／／属性
}
SubShader {
／／显卡 A 使用的子若色器
}
SubShader {
／／显卡 B 使用的子着色器
}
Fallback "Vertex Lit "

- Unity Shader的结构

	- shader名字

		- 通过在第一行使用这样的语句来命名自己的shader：Shader "Custom/MyShader "{  }

	- properties

		- Properties 语义块中包含了 一系列属性 (property)，这些属性将会出现在材质面板中。

	- SubShader

		- 每一个UnityShader文件可以包含多个SubShader语义块，但最少要有一个。 
		- 当Unity需要加载这个Unity Shader时，Unity会扫描所有的SubShader语义块， 然后选择第一个能够在目标平台上运行的SubShader。 如果都不支持的话， Unity就会使用Fallback语义指定的Unity Shader。
		- SubShader通常包含的定义如下
SubShader { 
／／可选的
[Tags] 
／／可选的
[RenderSetup) 
Pass { 
// Other Passes 
}

			- RenderSetup是状态
			- Tags是标签
			- Pass语义块

	- Fallback

- Unity Shader的形式

	- 表面着色器

		- 表面着色器定义在SubShader语义块中

	- 顶点、片元着色器

		- 被定义在Pass中

### 第四章 学习Shader所需的数学基础

- 笛卡尔坐标系

	- 二维笛卡尔坐标系
	- 三维笛卡尔坐标系

- 点和矢量
- 矩阵
- 坐标空间
- MVPC矩阵
- 法线变换
- Unity内置的变量

## 初级篇

### 第五章 开始Unity Shader学习之路

- 顶点、片元着色器的基本结构
- 模型数据从哪里来
- 顶点着色器怎么和片元着色器之间通信
- CG/HLSL语义
- Frame Debugger
- 渲染平台的差异
- Shader规范化

### 第六章 Unity中的基础光照

- 光源、吸收和散射
- BRDF光照模型
- 标准光照模型

	- 自发光emissive：当给定一个方向时，一个表面本身会向该方向发射多少辐射量
	- 高光反射specular：当光线从光源照射到表面的时候，会在完全镜面方向散射多少辐射量

		- 高光反射利用blinn-phong模型计算

	- 漫反射diffuse：当光线从光源照射到表面的时候，会向每个方向散射多少辐射量

		- 漫反射光照符合兰伯特定律

	- 环境光ambient：用于描述其他的间接光照

		- 在标准光照模型中，使用环境光来模拟间接光照

### 第七章 基础纹理

### 第八章 透明效果

## 中级篇

### 第九章 更复杂的光照

### 第十章 高级纹理

### 第十一章 让画面动起来

## 高级篇

### 第十二章 屏幕后处理效果

### 第十三章 使用深度和法线纹理

### 第十四章 非真实感渲染

### 第十五章 使用噪声

### 第十六章 Unity中的渲染优化技术

## 扩展篇

### 第十七章 Unity的表面着色器探秘

### 第十八章 基于物理的渲染

### 第十九章 Unity5更新了什么

### 第二十章 还有更多内容吗

## 计算机图形学第一定律：如果它看起来是对的，那它就是对的。

