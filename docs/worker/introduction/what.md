## 什么是web worker

***web worker 是运行在后台的 JavaScript，不会影响页面的性能。***


> JavaScript 是一个单线程语言，为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程。  

*热心市民 1问：那是不是JavaScript本质就是一个多线程语言了 ?*

**答：** 答应并不是，web worker只是主线程开辟的一个子线程，**且**子线程完全受主线程控制，**且**不得操作DOM，**且**还被阉割过。

*热心市民 2问：那啥都受制于人，那我要这铁棒有何用 ?*

**答：**在我们常规web端说白了更多的不是操纵DOM就是操纵DOM的路上，点来点去就是增删改查等等...我们都知道页面上的javascript在执行时会阻塞浏览器的响应，这非常影响用户体验，所以ajax应运而生了。ajax的出现使得页面在等待服务器响应的这段时间内不再发生阻塞，但是这仍然没有改变代码单线程执行的本质，这也意味着我们依旧不能把耗费时间的复杂运算放在页面上执行。而web worker的出现弥补了这个缺点。但是真正涉及到计算卡住主线程的实在不多，但是！并不是没有，比如：  

- <span style="color: #36c5bf">你遇到了大文件的上传<span>
- <span style="color: #36c5bf">又或者你写了下面这个代码： <span>  

```js
while(true) {
	console.log('xxx');
}
```
- <span style="color: #36c5bf">或者是大量的关键词匹配； <span>