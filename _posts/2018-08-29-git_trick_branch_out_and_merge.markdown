---
layout:     post
title:      "Git tricks"
subtitle:   "Branch Out and Merge"
date:       2018-08-29
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Git
    - Problem Handling
    - Study Notes
---

Say  you are working with a group of people on Master branch which is targeting current release, whereas you are doing performance fix which has separate logic and timeline, and is suggested to do source control on another branch.

*To get rid of unpushed commit:*
`git checkout master`
`git reset --hard 564a24f`

*Rebase a local branch to remote origin master branch:*
`git pull --rebase origin master`

*Merge local branch onto  master branch:*
`git branch temp`
`git checkout master`
`git merge temp`

```
+--------------+---+-------------------------+------------------+---------------------+
|  Class Type  |   | Can inherit from others | Can be inherited | Can be instantiated | 
|--------------|---|-------------------------+------------------+---------------------+
| normal       | : |          YES            |        YES       |         YES         |
| abstract     | : |          YES            |        YES       |         NO          |
| sealed       | : |          YES            |        NO        |         YES         |
| static       | : |          NO             |        NO        |         NO          |
+--------------+---+-------------------------+------------------+---------------------+
```

