---
layout: post
cover: assets/images/Keras.png
title: Keras Source Code to Solve Accuracy
date: 2020-03-07
tags:
    - Keras
author: Matt's Keras
---

先用一個<a href="https://github.com/keras-team/keras" target="_blank" color="#ff0000">Keras Source Code</a>來說明他的重要性，當然你也可以參考<a href="http://keras.io/" target="_blank" style="color:#ff0000">Keras Document</a>，但我覺得他寫的並不是很友善。接下來，我會特別針對在Keras裡面的Accuracy來試圖了解到底為什麼Accuracy可以小於0.5?<br/>

<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/sequential.py#L106">1.sequential.py: </a>他是在/keras/keras/engine folder的，裡面有<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/sequential.py#LC97">layer</a>,<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/sequential.py#LC106">model</a>,<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/sequential.py#LC232">predict_proba</a>,<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/sequential.py#LC254">predict_classes</a>...，但目前並不是我主要專攻的source code
<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/training.py">2.training.py</a>: 因為我想要了解model.evaluate[2](Accuracy)到底為什麼可以小於0.5，所以我就先了解在train.py裡面的<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/training.py#LC1357">evaluate method</a>，在最下面的return,有一個training_arrays.test_loop的method，我就接著往下看<br/>
<a href="https://github.com/keras-team/keras/blob/7a39b6c62d43c25472b2c2476bd2a8983ae4f682/keras/engine/training_arrays.py#LC342">3.training_array.py</a>: 直接看到function <span style="color:#6f42c1">fit loop</span>，然後因為我的evaluate的argument 的step是"None"，所以我們就先看到line434之後來看，以下有些可能要列一些：
<ul>
    <li>3.1 make_batches()</li>
    <li>3.2 slice_array()</li>
    <li>3.3 unpack_singleton</li>
    <li>3.4 isinstance</li>
    <li>3.5 enumerate</li>
    <li>3.6 hasattr</li>
    <li>3.7 scipy interp: 內插法</li>
</ul>
4.<span style="color:#2929a3">發現重要問題!!!</span>我覺得Keras 的 Accuracy 應該就是<a href="https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html" target="_blank">sklearn裡的accuracy_score</a>，且就是index 和 prediction的整數來比較，因為兩者幾乎一模一樣(ex: Keras Accuracy = 0.1983374643084505, accuracy_score = 0.19833746430693858)<br/>

5.[::-1]是反向執行<br/>

6.今天有跟同學們討論，他們覺得如果要把discontinuous MC put into Continuous energy Model來train出來的結果會比較有意義，乍看之下似乎有些道理，但我馬上發現一些問題，Total energy in each event，標題上的GeV(如20GeV,100GeV,300GeV...)，pion其實都是從0GeV~200GeV，而electron則是在標題的GeV以高斯範圍顯示，很明顯的在200GeV以上，其實preselection已經完全沒有意義了，所以我明天必須跟老師討論:到底在discontinuous energy裡的<span style="color:#ff0000">preselection 到底要不要用???</span>，因為同學他們都說如果model有preselection，input 的data/MC也要做preselect?<br/>

7.以下有幾個我不是很熟悉的numpy function，要有所記錄一下:
<ul>
    <li>7.1 <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros_like.html" target="_blank">np.zeros_like</a>: 將array value通通變成0</li>
    <li>7.2 <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.unique.html" target="_blank">np.unique</a>: 在list,array...重複出現的value就直接剔除，留下唯一的value</li>
    <li>7.3 <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.argsort.html" target="_blank">np.argsort</a>: 應該是排序，但我還是不太了解他跟sort有何差別QQ</li>
    <li>7.4 <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.cumsum.html" target="_blank">np.cumsum</a>: 把之前和此點的value累加後再放入此value</li>
    <li>7.5 <a href="https://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.diff.html" target="_blank">np.diff</a>: 把現在的value減去前一個value後再放入現在的value之中</li>
</ul>