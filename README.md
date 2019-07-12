# GLSurface
demo code for remote（seperate process） GLSurface Renderin



Surface是EGL的“画布”，一块内存buffer加上config，就可以生成一块画布
config包含了display的属性，包括颜色深度，位长等
surface类型，window，pixmap，pbuffer


以采集Camera数据后，进行绘制为例
1. 获取界面对象GLSurfaceView
2. setRenderer
3. 收到onSurfaceCreated回调，在回调中准备如下工作
    3.1. 申请一块buffer，rgb or nv21
    3.2. addCallbackBuffer
    3.3  setPreviewCallbackWithBuffer
    3.4  startPreview
4. 收到相机预览帧onPreviewFrame，调用GLSurfaceView.requestRender，通知界面渲染
5. 收到render的回调onDrawFrame，在此函数中可以用buffer或者textureID进行纹理绘图，然后调用SurfaceTexture.updateTexImage通知消耗buffer



reference:
《EGL Specification 1.0 的研读笔记》
https://www.cnblogs.com/bpasser/archive/2011/09/26/2191710.html

使用GLSurface绘制相机预览
https://www.jianshu.com/p/affeb48e465c
apk代码的原型

Android sharing SurfaceTexture between two processes
https://stackoverflow.com/questions/33222621/android-sharing-surfacetexture-between-two-processes

一个demo
https://github.com/Faceunity/FULiveDemoDroid

玩转Android Camera开发
https://blog.csdn.net/yanzi1225627/article/details/33339965/
