# 左边被挤压或右边的子元素过宽导致界面异常
```
.main{
  display: flex
}
.main .left{
  width: 300px;
  flex-shrink: 0; // 防止被挤压
}
.main .right{
  flex: 1;
  overflow: hidden; // 内部元素超过其宽度使其布局异常
}

```
