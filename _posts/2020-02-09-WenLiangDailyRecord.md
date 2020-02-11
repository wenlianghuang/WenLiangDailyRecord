---
layout: post
cover: assets/images/welcome.jpg
title: Start the second blog in github
date: 2020-02-09
tags: Diary
author: wenliang
---

<h2>Overview in 20200209</h2>
在github wibsite中有些我可能不太了解的事，要做一些簡單的紀錄

<p>1.在post.html & page.html的:
在_post directory下一定有些特定的varialbe(ex:layout, tag, title...)，而在_layout裡的.html file就是以<font style="color:#7FFF00">post & page</font>為class，接著在page下有各種的varialbe</p>
<ul>
    <li>1.1 page.tags.size:看一下是哪一種的blog與此種blog的數量</li>
    <li>1.2 我還每有看懂related article...</li>
    <li>1.3 site.data.authors:在page下有很多不同種類的authors,其細節大部分都來自<font style="color:#7fff00">authors.yml</font>，而在for loop中，variable author其實有隱含<font style="d2691e">array</font>的性質</li>
    <li>1.4 social box我也還沒看懂...</li>
</ul>

<hr>
<p>2.每篇的最下邊都有一個小小的貼圖和他所在的屬性和tag的類別，其實這就是不同種的author,歸在<font style="color:#7fff00">authors.yml</font>,而這個file中目前有三種class:hanuman,krishna,Matt.每個class裡面也有幾個不一樣的variable,以下我列出幾個重要的variable:</p>
<ul>
    <li>2.1 username: 是在authors.yml中類別名稱</li>
    <li>2.2 name: 在每篇下author實際顯示的名字</li>
    <li>2.3 bio: username的簡介</li>
    <li>2.4 assests: authors旁邊的小找片</li>
</ul>
<hr>
<p>3.variable "author" in post.html (大概line 13x左右開始),要寫出author的名字和他的biography，裡面大部分都沒有問題，可是我突發起想說:既然在.html裡面就已經有for,if之類的，我為什麼不將javascript放在裡面做出類似的效果和一樣的網站呈現?但<font style="color:#7fff00">第一個難題</font>就是在for loop中還有"<div>"，而我目前是先利用<a href="https://stackoverflow.com/questions/11398522/create-a-div-using-loop" style="color:ffd633" target="_blank">目前的解決方式</a>來處理</p>

<hr>
<font style="color:#7fff00">未完待續</font>