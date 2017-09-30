---
layout:     post
title:      "Python Tricks"
date:       2017-08-12 12:00:00
author:     "BoyuanZH"
header-img: "img/post-bg.jpg"
tags:
    - Language
---

## Python Tricks

> **String**

* ```strip([char]), lstrip([char]), rstrip([char])```
	* if ```[char] = "abc"```, then strip any combination of them in the original String.

* ```"".join([string])```
* ```"a, b, c".split(",")```
* ```"Total number of col is {} and row is {}".format(1, 2)```
* ```"Total number of col is {} and row is {}".format(*[1, 2])```
* ```setA.issubset(setB)```
    * Wrong: setA in setB

* ```"%d:%02d" % (h, m)```, output is in format of `"2:05"`
* Python has no built-in `right logic shift`, customized a logic right shift as follow:

    ```
    def rshift(num, x):
            if num >= 0: return num >> x
            if num < 0: return (num + 0x100000000) >> x
    ```
* 