---
layout: post
title: Introduction of C Sharp
cover: assets/images/welcome.jpg
date: 2020-02-10
tags: Diary
author: wenliang
---

C# Generic:

其實就跟template很像,直接用個class example來看:<br/>
```cs
using System;  
namespace CSharpProgram  
{  
    class GenericClass<T>  
    {  
        public GenericClass(T msg)  
        {  
            Console.WriteLine(msg);  
        }  
    }  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            GenericClass<string> gen   = new GenericClass<string> ("This is generic class");  
            GenericClass<int>    genI  = new GenericClass<int>(101);  
            GenericClass<char>   getCh = new GenericClass<char>('I');  
        }  
    }  
}
```
小提醒:c# 語法highlighting 是用<font style="color:#7fff00">'''cs'''</font>
<hr>


