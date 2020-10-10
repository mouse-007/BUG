# 请求失败,报错ERR_UNESCAPED_CHARACTERS

> 原因：url中包含了中文字符

> 解决方案：使用encodeURI(url)编码
