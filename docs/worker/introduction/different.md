## 与主线程的区别
你可以在worker 线程中运行任意的代码，但注意存在一些例外：直接在 worker 线程中操纵 DOM 元素；或使用window 对象中的某些方法和属性。大部分 window 对象的方法和属性是可以使用的，包括 WebSockets，以及诸如 IndexedDB 和 FireFox OS 中独有的 Data Store API 这一类数据存储机制。
前面 [什么是web worker ?](/worker/introduction/what.md) 已经提过了，web worker存在被阉割的情况，所以在使用前必须要弄清楚相关的支持。<br><br>
下面是较为常见的：
<table id="tab">
	<tbody>
		<tr>
			<th></th>
			<th>Firefox</th>
			<th>IE</th>
			<th>Chrome / Opera</th>
			<th>Safari</th>
		</tr>
		<tr>
			<td>Console API</td>
			<td> 38 (38) </td>
			<td>YES</td>
			<td>YES</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>Fetch</td>
			<td> Mostly in 34 (34) behind pref, although a few features are later.</td>
			<td>NO</td>
			<td>42, 41 behind pref</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>Promise</td>
			<td> 28 (28) </td>
			<td>Yes</td>
			<td>Yes</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>WebSocket</td>
			<td> 37 (37) </td>
			<td>11.0</td>
			<td>Yes</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>Worker</td>
			<td> 3.5 (1.9.1) </td>
			<td>10.0</td>
			<td>NO</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>XMLHttpRequest</td>
			<td> 
				Basic: 3.5 (1.9.1)<br><br>
				response and responseType are available since 10 (10)<br><br>
				timeout and ontimeout are available since 13 (13)<br>
			</td>  
			<td>YES</td>
			<td>YES</td>
			<td>YES</td>
		</tr>
		<tr>
			<td>...</td>
			<td>...</td>  
			<td>...</td>
			<td>...</td>
			<td>...</td>
		</tr>
	</tbody>
</table>

详情可以参照 [Workers可以使用的函数和类](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API/Functions_and_classes_available_to_workers)

这里打个 ***？*** <u>**indexDB** 属于挂载在window对象下的，但是官方文档却说相关支持</u>
