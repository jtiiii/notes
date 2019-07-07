# Javascript 再学习

由于工作中也渐渐开始接触一些前端需求的功能。但是自身本身是专注于后台开发的。对于前端也不是很熟。但觉得自己前端开发效率很低，特此再开一次javascript学习计划。主要就是补充自己欠缺的部分知识。并非是完整的

笔记内容摘自泽卡斯（Zakas.NicholasC.）.JavaScript高级程序设计(第3版)(图灵程序设计丛书).人民邮电出版社.Kindle版本.

只是强调补全一些知识，并非所有javascript基础部分。不适合初学者。



# 什么是ECMAScript？

由ECMA-262定义的ECMAScript与Web浏览器没有依赖关系。实际上，这门语言本身并不包含输入和输出定义。ECMA-262定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。我们常见的Web浏览器只是ECMAScript实现可能的宿主环境之一。宿主环境不仅提供基本的ECMAScript实现，同时也会提供该语言的扩展，以便语言与环境之间对接交互。而这些扩展——如DOM，则利用ECMAScript的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。前面介绍过的Node以及众所周知的AdobeFlash也都是宿主环境。既然ECMA-262标准没有参照Web浏览器，那它都规定了些什么内容呢？大致说来，它规定了这门语言的下列组成部分：语法类型语句关键字保留字操作符对象ECMAScript就是对实现该标准规定的各个方面内容的语言的描述。JavaScript实现了ECMAScript，AdobeActionScript同样也实现了ECMAScript。

泽卡斯（Zakas.NicholasC.）.JavaScript高级程序设计(第3版)(图灵程序设计丛书)(Kindle位置329-334).人民邮电出版社.Kindle版本。

> 简单的说ECMAScript就是各大Web浏览器所执行的Script的一些规定和标准。