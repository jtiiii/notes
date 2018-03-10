# 什么是Node?

Node是一个JS的运行环境，类似JVM，采用的V8引擎的运行环境，能让JS脱离浏览器进行运行。

Example:

Hello-world.js:

```javascript

```



```shell
$node example.js
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

