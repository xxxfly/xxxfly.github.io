---
layout:     post
title:      对请求参数的键值对进行ASCⅡ排序
subtitle:   对请求参数的键值对进行ASCⅡ排序
date:       2018-03-01
author:     zx
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - .NET
    - C#
    - ASCⅡ排序
---


# 对请求参数的键值对进行ASCⅡ排序
对接别人接口的时候，经常遇到一种简单的加密，就是对请求的参数列表进行ASCⅡ排序之后，加上双方约定的KEY值进行MD5加密。

在C#里面可以直接使用  SortedDictionary〈T,T〉进行排序。

示例代码

```C#
public void Test() {
    SortedDictionarysorted_dic = new SortedDictionary();
    //请求参数列表
    sorted_dic.Add ("busi_channel", busi_channel);
    sorted_dic.Add ("account_id", account_id);
    sorted_dic.Add ("pay_channel", pay_channel);
    sorted_dic.Add ("request_seq", request_seq);
    sorted_dic.Add ("pay_type", pay_type);
    sorted_dic.Add ("request_time", request_time);
    sorted_dic.Add ("pay_amount", pay_amount);
    sorted_dic.Add ("notify_url", notify_url);
    sorted_dic.Add ("bank_id", bank_id);
    sorted_dic.Add ("client_ip", client_ip);
 
    string strSource = "";
    //自动按ASCⅡ排序
    foreach (KeyValuePairitem in sorted_dic) {
        strSource += item.Key + "=" + item.Value + "&";
    }
    //加密KEY          
    strSource += "key=helloworld";
    //请求参数MD5加密
    string sign = SecurityUtility.GetMD5 (strSource);
}
```

其中GetMD5方法如下：
```C#
public static string GetMD5 (string sourceString) {
    return FormsAuthentication.HashPasswordForStoringInConfigFile (sourceString, "MD5");
}
```
