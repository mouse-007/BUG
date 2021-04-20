> bug描述
 ```<input type="file"/> ```在chrome浏览器选择文件时会偶发（未响应）
> 可能原因（不知道咋验证所以是可能）
属性 accept 设置为 image/* 会有安全检查，很慢所以卡死（度娘与google的）
> bug修复
设置 accpet 属性为 image/jpeg, image/jpg, image/png 这些属于白名单中的 所以很快

ps: 以上内容来源网络，真实性有待考究。
