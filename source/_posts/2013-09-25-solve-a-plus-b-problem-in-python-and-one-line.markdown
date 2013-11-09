---
layout: post
title: "Solve A+B Problem in python &amp; one line"
date: 2013-09-25 02:23
comments: true
categories: python, ACM
---

Classical ACM/ICPC Problem

one test case is easy, how to support multi- test cases?

ex.
``` python
# Input
1 2
2 4

# Output
3
6

```

in python 2.x

``` python
from __future__ import print_function; import sys; map(lambda x: print(sum(x)), [map(int, line.split()) for line in sys.stdin]);
```

You can test it on the Online Judge. :)

