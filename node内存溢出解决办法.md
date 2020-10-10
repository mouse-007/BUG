# Node部分
1. 服务器编译内存溢出 ([参考地址](https://www.dazhuanlan.com/2019/12/05/5de80af203282/
))

 + 通用
 ___
```
node --max_old_space_size=2048 xxx.js
```
 + node v8.x+
 ___
	```
	 export NODE_OPTIONS=--max_old_space_size=2048 // linux
	 set NODE_OPTIONS=--max_old_space_size=2048 // window ，或者系统变量里添加NODE_OPTIONS=--max_old_space_size=2048
	```
  必须要确认该系统环境变量已经生效了，可以用echo $NODE_OPTIONS来校验。验证扩展内存是否生效。
  ___
  ```
  const v8 = require('v8'
  console.log(v8.getHeapStatistics())
  /* 输出
   {
   	total_heap_size: 5009408,
   	total_heap_size_executable: 1048576,
   	total_physical_size: 3449648,
   	total_available_size: 2194521344,
   	used_heap_size: 2411032,
   	heap_size_limit: 2197815296,
   	malloced_memory: 8192,
   	peak_malloced_memory: 410288,
   	does_zap_garbage: 0
 }*/
  ```
其中的heap_size_limit就是老生代可以使用的最大内存，单位是Byte。
 + 使用hack技巧解决特殊情况
 ```
	 #!/bin/sh 
	":" //# comment; exec /usr/bin/env node --max_old_space_size=2048 "$0" "$@"

	const program = require('commander')

	program
	  .version('0.1.0')
	  .command('start')
	  .action(function () {
		// start process...
	  })

	program.parse(process.argv)

	...
 ```
 解释一下：
  	 + 第一行是指定使用shshell。
   	+ 第二行其实分为两个部分：":" //# comment; 和 exec /usr/bin/env node --max_old_space_size=2048 "$0" "$@"。前半部分是Bourne Shell内置支持的写法，只需要了解#和;之间是可以写注释的就行了；后半部分是使用Node执行相关的命令，$0传递一个参数0，$@传递其他额外的参数。
		这样，就能正常传递参数了。







		
