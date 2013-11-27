# 专题：JavaScript的装载与执行

**浏览器对JavaScript的运行有两大特性：**

* 载入后马上执行
* 执行时会阻塞页面后续的内容（包括页面的渲染、其它资源的下载）

### 如何异步载入JavaScript？

**document.write方式**

> alert.js

	alert("Hello World");

> test1.html

	<!DOCTYPE html>
	<html>
	<head>
	    <script type="text/javascript">
	        function loadScript(scriptFileName) {
	            document.write('\<script type="text/javascript" src="' + scriptFileName + '"\>\</script\>');
	            alert("loadScript() exit...");
	        }
	        var scriptFileName = 'alert.js';
	        loadScript(scriptFileName);
	        alert("loadScript() finished");
	    </script>
	    <script type="text/javascript">
	        alert('the second script tag');
	    </script>
	</head>
	<body>
	    <h1>Hello World</h1>
	</body>
	</html>

**Chrome浏览器执行过程：**

<ol>
	<li>alert: loadScript() exit...</li>
	<li>alert: loadScript() finished</li>
	<li>alert: Hello World</li>
	<li>alert: the second script tag</li>
	<li>body标签中的H1标签显示出来</li>
</ol>

我们发现，在Chrome浏览器下，对于在同一个script标签的JavaScript代码来说，alert.js确实是异步载入了，但对于整个页面来说，
这个还是会阻塞。第二个script标签中代码的执行晚于alert.js代码的执行，\<h1\>Hello World\</h1\>标签的渲染也是最后完成。

**Firefox浏览器执行过程：**

<ol>
	<li>alert: Hello World</li>
	<li>alert: loadScript() exit...</li>
	<li>alert: loadScript() finished</li>
	<li>alert: the second script tag</li>
	<li>body标签中的H1标签显示出来</li>
</ol>

我们发现，在Firefox浏览器下，alert: Hello World是最先执行的，也就是说，在同一个script标签中，document.write方式并没有
起到异步载入的功能。



















