title: Integer Normalization
date: 2014-11-12 18:08:05
categories: Programming
tags:
---
Sometimes, we need to draw diagrams of serials of integer values, but with Y axis value from 0 to 100.
So if the actual value is too large or too small, we need to normalize it to between 0 and 100, so that to fit into the diagram better.
For example, if the actual value is 998, then we need to scale it by 0.1 and the value in diagram is 99.8.
<!--more-->
Here is the C# code I used to get the scale (s) from a given value (M). 
``` csharp
double s = 1.0;
if (!M.Equals(0))
{
  s = Math.Pow(10, Math.Floor(Math.Log10(100/M)));
}
```

I also proved this by mathematics. That's the most interesting part :)
![](/img/post/ProveIntegerNormalization.png)