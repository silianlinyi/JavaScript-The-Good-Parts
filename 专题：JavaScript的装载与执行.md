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
<ol>







