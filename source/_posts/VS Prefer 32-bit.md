title: Visual Studio Prefer 32-bit Trick
date: 2015-04-08 18:57:17
categories: Programming
tags:
---
When you create a new C# application project in Visual Studio 2012, there's an option called "Prefer 32-bit" for platform target Any CPU.
![](/img/post/Prefer32Bit.png)

Since we're in the 64-bit world, **simply make sure you uncheck the option**. Otherwise, you will find your program is actually running as a 32-bit process even in 64-bit OS, appeared with name of something like **"MyApp.exe *32"** in the Task Manager.

The only exception case is that you do want your project to be 32-bit, for example, you've referenced some other dll which is not 64-bit compatible.

Refer to this artical for more detailed explaination:
http://blogs.microsoft.co.il/sasha/2012/04/04/what-anycpu-really-means-as-of-net-45-and-visual-studio-11/
