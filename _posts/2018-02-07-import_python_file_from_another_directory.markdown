layout:     post
title:      "Import Python File From Another Directory"
subtitle:   "Learning From Work Assignments"
date:       2018-02-07
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:

    - python
    - Study Notes
---
In this walk-through, I will explain how to import python file from another directory.

Imagine we have following file structure:

```
Analysis/
	Main.py
	HelperFunctions/
		FunctionGroupA.py
		FunctionGroupB.py
```

Main.py is the main scripts to run the analysis, where we need to import multiple functions from two other python files under the HelperFunctions folder.

Directly import as following statement raise ModuleNotFound error, since HelperFunctions is not considered as a package:

```python
from HelperFunctions import FunctionGroupA, FunctionGroupB
```

In order to make python treat HelperFunctions as a package, we need to create a __init__.py file inside the HelperFunctions folder. New directory structure is as following:

```
Analysis/
	Main.py
	HelperFunctions/
		__init__.py
		FunctionGroupA.py
		FunctionGroupB.py
```

And HelperFunctions/__init__.py has following lines in it:

```python
import .FunctionGroupA
import .FunctionGroupB
```

>*Reference:*
>*   5.4.2 https://docs.python.org/3/reference/import.html