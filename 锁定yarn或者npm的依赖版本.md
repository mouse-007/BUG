> 1.项目中的依赖中国的依赖升级导致项目无法正常打包或者开发
     解决方案: 在package.json中增加resolutions项
     ```
        // 例如锁定fs的版本号为1.2.0
        ...
        "resolutions": {
            "fs": "1.2.0"
        }
     ```
> 2.固化依赖的版本
   yarn会自动生成yarn.lock文件
   npm执行
   ```
    // 生成依赖  默认不包括dev dependencies
    npm shrinkwrap
    // 将dev-dependencies计算在内
    npm shrinkwrap--dev 
   ```
