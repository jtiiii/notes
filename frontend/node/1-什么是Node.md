# 什么是Node?

Node是一个JS的运行环境，类似JVM，采用的V8引擎的运行环境，能让JS脱离浏览器进行运行。

Example:

Hello-world.js:

```javascript
exports.printMsg = function(){console.info("Hello World!");};
```

使用node执行

```shell
$node Hello-world.js
#// Hello World!
```



Node使用了NPM作为包管理器。

Node可以直接编写HTTP微服务。

Example:

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`服务器运行在 http://${hostname}:${port}/`);
});
```



Node是将Javascript完全脱离浏览器执行的的一个js环境，node实现了可以用js来做后端。不过node并不能做前端，但可以用来做构建前端的工具。

Node和前端几乎没什么关系。