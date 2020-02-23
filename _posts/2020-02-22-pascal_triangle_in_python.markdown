---
layout: post
title:      "Pascal triangle in Python"
date:       2020-02-22 03:57:57 +0000
permalink:  pascal_triangle_in_python
---


```
    def generate(self, numRows: int) -> List[List[int]]:
        if numRows==0:
            return []
        c=[]
        a=[1]
        c.append(a)
        for i in range(1,numRows):
            b=[1]
            for j in range(1,i):
                b.append(a[j-1]+a[j])
            b.append(1)
            a=b
            c.append(a)
        return c
```

This is the code for Pascal triangle in Python. It is short and neat, because there is no need to define any data types.
