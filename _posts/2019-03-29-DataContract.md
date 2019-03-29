---
layout:     post
title:      数据契约
subtitle:   DataContract
date:       2019-03-29
author:     zx
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - .NET
    - C#
---

## 数据契约
### DataContract

服务契约定义了远程访问对象和可调用的方法  

数据契约则是服务端和客户端之间要传送的自定义数据泛型

一旦声明一个类型为DataContract，那么该类型就可以被序列化在服务端和客户端之间传送
```C#
[DataContract]
public class UserInfo
{
}
```
只有声明为DataContract的类型的对象可以被传送，且只有成员属性会被传递，成员方法不会被传递。  

WCF对声明为DataContract的类型提供更加细节的控制，可以把一个成员排除在序列化范围以外，也就是说，客户端程序不会获得排除在外的成员的任何信息，包括定义和数据。  

默认情况下，所有的成员属性都被排除在外，因此需要把每一个要传递的成员声明为DataMember。  
```C#
[DataContract]
public class UserInfo
{
     [DataMember]
     public string UserName
     {
          get;
          set;
     }
     [DataMember]
     public int Age
     {
         get;
         set;
     }
     public string Zodiac
     {
         get;
         set;
     }
}
```

上面这段代码把UserInfo类声明为DataContract，将UserName、Age声明为DataMember（数据成员）。将Zodiac成员没有声明为DataMember，因此在交换数据时，不会传输Zodiac的任何信息。  

DataContract也支持Name/Namespace属性，如同ServiceContract，Name和Namespace可以自定义名称和命名空间，客户端将使用自定义的名称和命名空间对DataContract类型进行访问。  

```C#
[DataMember(Name="Name")]
public string UserName
{
    get;
    set;
}
```
除了Name和Namespace以外，DataMember还有以下参数：  
（1）IsRequired：值为true时，要求序列化引擎检查对象是否存在该值；若无，则会有异常抛出。  
（2）Order：bool类型值，值为true时，序列化和反序列化过程将会按成员定义的顺序进行，这对依赖成员位置的反序列化过程无比重要。  
（3）EmitDefaultvalue：为成员属性设置一个默认值。  
