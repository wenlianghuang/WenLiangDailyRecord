---
layout: post
title: Introduction of C Sharp
cover: assets/images/CSharp.jpeg
date: 2020-02-10
tags: 
    - C#
author: Matt's csharp
permalink: "2020-02-10-CSharp-Intro.html"
---
<h2>預先提醒:  Code highlight 是利用<span class="languagecolor">```最頭最尾各三個頓號，中間是用副檔名```(把code內容也框起來)</span></h2>
<!--
<h3><span style="color:#3366ff">C# Generic</span></h3>:
-->
<h3><span class="languagemethod">C# Generic:</span></h3>

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
<a href="https://www.javatpoint.com/c-sharp-generics">參考</a>

<hr>

<h3><span class="languagemethod">C# Delegate: </span></h3>

特殊功能之一，比較像在C/C++有dynamic array，只是C/C++是pointer，而C# delegate是reference，而參數也可以用variable或是method帶入delegate，現面我還是用example來看

```cs
using System;
delegate int Calculator(int n);
namespace DelegateEx
{
    class DelegateExample
    {
        static int number = 100;
        public static int add(int n){
            number = number + n;
            return number;
        }

        public static int mul(int n){
            number = number * n;
            return number;
        }

        public static int getNumber(){
            return number;
        }
        static void Main(string[] args)
        {
            Calculator c1 = new Calculator(add);
            Calculator c2 = new Calculator(mul);
            c1(20);
            Console.WriteLine("After c1 delegate, Number is: " + getNumber());
            c2(3);
            Console.WriteLine("After c2 delegate, Number is: " + getNumber());
            

        }
    }
}
```
<a href="https://www.javatpoint.com/c-sharp-delegates">參考</a>

<hr>

<h3><span class="languagemethod">C# Lambda Expression and Anonymous Method: </span></h3>

<h4>Lamdba Expression:跟之前的deleget有關,利用(intput-parameter)=>expression，最後再垂回給deleget，以下請看範例</h4>

```cs
using System;
namespce LambdaExpression{
    class Program{
        deleget int Square(int num);
        static void Main(string [] args){
            Square GetSquare = x => x*x
            int j = GetSquare(5);
            Console.WriteLine("Square is: " + j);
        }
    }
}
```
<a href="https://www.javatpoint.com/c-sharp-anonymous-function">參考</a>

<h4>Anonymous Method:跟Lambda Expression很像，但他可以"隱匿"所有的變數和參數，我們還是由下面來當範例</h4>

```cs
using System;
namespace AnonymousMethod{
    class Program{
        public deleget void AnonymousFun();
        static void Main(string [] args){
            AnonymousFun fun = deleget(){
                Console.WriteLine("This is anonymous function");
            }
        }
    }
}
```
<a href="https://www.javatpoint.com/c-sharp-anonymous-function">參考</a>

<hr>

<h3><span class="languagemethod">C# MultiThread
