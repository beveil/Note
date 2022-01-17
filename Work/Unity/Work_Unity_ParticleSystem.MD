### 1：Particle System RenderMode选择Mesh在AB环境下不显示的问题：  
原因: PariticleSystem对外提供了一系列Mesh顶点修改、变化以及Shader属性修改的功能,常用的如: Color, StartColor 属性, 如果使用Mesh渲染而在导入FBX时未勾选Read/Write Enable, 则**可能**会在运行时会出现特效看不见的问题

以下是搜索出的一些结果:
![官方手册截图](/Pic/particleSystem1.png)
![官方论坛回复](/Pic/particleSystem2.png)

总结：
使用Mesh作为Render的粒子以下情况对应的Mesh要勾上Read/Write Enable  
1. 粒子系统中如果用到Shape、Color Over Lifetime、Color By Speed 模块等(用到了Mesh 的顶点信息)
2. Render模块中未勾上GPU Instance

注意事项:  
* 如果是非AB方式打包，打包时Unity发现某个Render Mode为Mesh的ParticleSystem使用了Mesh信息而你导入时没有勾选Read/Write Enable的话，会在打包过程中自动使这个属性生效。
* AB打包过程中，如果该粒子特效和Mesh在一个AB包中，Unity也会使该属性生效，否则不生效(运行时无法看见特效)

