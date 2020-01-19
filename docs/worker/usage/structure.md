## worker初体验

+ 创建以 *.worker.js* 结尾的文件，例如：bond.worker.js


##### 主线程  

主线程采用new命令，调用Worker()构造函数，新建一个 Worker 线程。

```js
// 实例化 worker
const worker = new Worker('bond.worker.js');
// Worker()构造函数的参数是一个脚本文件，该文件就是 Worker 线程所要执行的任务。
```
- <span style="color: #36c5bf">worker.postMessage()<span>   

worker.postMessage()方法的参数，就是主线程传给 Worker 的数据。它可以是各种数据类型，包括二进制数据。
```js
worker.postMessage('Hello World');
worker.postMessage({xxx: 'xxx', xxx1: ['xxx1']});
```

- <span style="color: #36c5bf">worker.onmessage()<span>  

主线程通过worker.onmessage指定监听函数，接收子线程发回来的消息。
```js
worker.onmessage = (event) => {
	// doSomething();
}
```

- <span style="color: #36c5bf">worker.onmessage()<span>  

当 worker 完成任务以后，主线程就可以把它关掉。
```js
worker.terminate();
```


*上述已经描述了主线程的跟worker线程的通讯，那么接下来就是worker线程怎么应答主线程相关的信息*

##### worker线程

> self代表子线程自身，即子线程的全局对象;  

- <span style="color: #36c5bf">self.onmessage()<span>  

在 worker 线程内部需要有一个监听函数，监听message事件。  
```js
self.onmessage = (data) => {
	// doSomething();
}
```
- <span style="color: #36c5bf">self.postMessage()<span>  

worker向主线程发送通讯，
```js
// worker线程
self.postMessage();

// 主线程
worker.onmessage = (data) => {};
```

- <span style="color: #36c5bf">self.close()<span>  

worker 关闭内部自身



