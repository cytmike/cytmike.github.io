---
layout: post
title:      "Python swap"
date:       2020-01-25 16:21:24 -0500
permalink:  python_swap
---


To swap 2 variables, it is possible to do
```
a,b = b,a
```

It is much easier than other traditional languages where a temporary variable is required:

```
t=a
a=b
b=t
```

It is more powerful when this is also possible
```
a,b=b,a+b
```

3 or more variables is also possible
```
a,b,c,d=b,c,a,d
```

Swap some elements in a list
```
list[1],list[8]=list[8],list[1]
```


