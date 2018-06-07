### promise

    
    const wait = ms => new Promise(resolve => setTimeout(resolve, ms));
    wait(10000).then(() => saySomething("10 seconds")).catch(failureCallback);
    
### 时序
为了避免意外，即使是一个已经变成 resolve 状态的 promise，传递给 then 的函数也总是会被异步调用：

    Promise.resolve().then(() => console.log(2));
    console.log(1); // 1, 2
    
传递到then中的函数被置入了一个微任务队列，而不是立即执行，这意味着它是在JavaScript事件队列的所有运行时结束了，事件队列被清空之后才开始执行：

    const wait = ms => new Promise(resolve => setTimeout(resolve, ms));
    wait().then(() => console.log(4));
    Promise.resolve().then(() => console.log(2)).then(() => console.log(3));
    console.log(1);
    
    
    https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises
    https://developers.google.com/web/fundamentals/primers/promises
    https://segmentfault.com/a/1190000007535316
