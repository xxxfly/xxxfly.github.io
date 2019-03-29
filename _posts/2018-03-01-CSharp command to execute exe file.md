---
layout:     post
title:      C#执行exe文件的命令
subtitle:   C#执行exe文件的命令
date:       2018-03-01
author:     zx
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - .NET
    - C#
    - 命令
---


# Csharp执行exe文件的命令
## 使用代码执行exe文件的命令
下载的是视频处理的 ffmpeg 的exe文件。有很强大的音视频解码能力，具体了解的话可以学习雷神的博客，里面讲解非常详细。
[博客地址](http://blog.csdn.net/leixiaohua1020/article/details/15811977/" 博客地址"){:target="_blank"} 

这里我是用来解析视频文件信息的

代码如下
```C#
using (System.Diagnostics.Process pro = new System.Diagnostics.Process())
{
    pro.StartInfo.UseShellExecute = false;
    pro.StartInfo.ErrorDialog = false;
    pro.StartInfo.RedirectStandardError = true;
    pro.StartInfo.CreateNoWindow = true; //不显示windows命令窗
    string ffmpegPath = AppDomain.CurrentDomain.BaseDirectory + "ffmpeg.exe";  //获取物理路径
    pro.StartInfo.FileName = ffmpegPath;
 
    pro.StartInfo.Arguments = "-i " + "\"" + filePath + "\"";   //执行命令
    pro.Start();
    System.IO.StreamReader errorreader = pro.StandardError;
    pro.WaitForExit(1000);
    string result = errorreader.ReadToEnd();  //读取命令的结果
 
}
```