### node

### koa

koa是基于node.js的web框架，可以搭建web应用。一般用于搭建http服务。
最简单的：  

    const Koa = require('koa');
    const app = new Koa();
    app.listen(3000);

使用node运行该脚本 node xxx,  http://localhost:3000查看

### koa context对象
koa提供一个context对象，表示一次对话的上下文（包括 HTTP 请求和 HTTP 回复）。通过加工这个对象，就可以控制返回给用户的内容。

    const Koa = require('koa');
    const app = new Koa();

    const main = ctx => {
      ctx.response.body = 'Hello World';
    };

    app.use(main);
    app.listen(3000);

### koa-route 封装好的koa路由

    const route = require('koa-route');

    const about = ctx => {
      ctx.response.type = 'html';
      ctx.response.body = '<a href="/">Index Page</a>';
    };

    const main = ctx => {
      ctx.response.body = 'Hello World';
    };

    app.use(route.get('/', main));
    app.use(route.get('/about', about));
    
    
### koa-router 也是个路由，用的多一些

