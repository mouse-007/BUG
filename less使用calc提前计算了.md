对于前端er来说，Less或Sass已经是一项必备的基本技能，有了这个利器，可以省下前端开发者的很多编码时间，让你写CSS如行云流水一般，然后最近我在Less里加入calc时确发现了有点问题，我在Less中这么写：
```
div {width : calc(100% - 30px);}
```
结果Less把这个当成运算式去执行了，结果给我解析成这样：
```
<span style="font-size:14px;">div {width: calc(70%);}</span>
```
当时我就郁闷了，怎么会产生这样的现象呢？后来各种查，是由于less的计算方式跟calc方法有重叠，两者在一起有冲突，于是，我在Less中把calc的写法改写成下面这样：
```
<span style="font-size:14px;">div {width : calc(~"100% - 30px");}</span>
```

然而，把30px替换为一个变量，怎么写呢？

```
　　div {
　　@diff : 30px;
　　width : calc(~"100% - " + @diff);
　　}
```
　　这么写Webstorm没有报错，但grunt-less报错了：
```
　　C:\Users\zhong\WebstormProjects\test>grunt less
　　Running "less:development" (less) task
　　>> ParseError: Unrecognised input in style.less on line 4, column 2:
　　>> 3    @diff : 30px;
　　>> 4    width : calc(~"100% - " + @diff);
　　>> 5 }
　　Warning: Error compiling style.less Use --force to continue.
　　Aborted due to warnings.
```
　　于是这么写：
```
　　div {
　　@diff : 30px;
　　width : calc(~"100% - " @diff);
　　}
```
　　顺利编译过去，但Webstorm却老是提示语法错误，虽然也能编译但看着文件有一个错误提示心里老

感觉不爽，找半天也没发现Webstorm如何调试语法提示错误设置
　　于是，改成如下写法：
  ```
　　div {
　　@diff : 30px;
　　width : calc(~"100% - @{diff}");
　　}
  ```
　　这种写法又能编译，Webstorm里又不报错，所以我比较喜欢用这种写法，如此，便不会再有任何问题了。

PS:在这里提供一个工具网站，http://tool.lu/css/(#http://tool.lu/css) ，能提供各种CSS以及其他语言的格式化，往往less编译后的css文件的格式并不是我们所需要de
