打包后无法正常运行.mjs解析异常（@babel/runtime）
环境：roadhog 
修复：
增加webpack.config.js文件
内容：
const path = require('path');
module.exports = function (config, env) {
    config.module.rules.forEach(item => {
        if (item.loader && item.loader.indexOf('url-loader') > -1) {
          item.exclude.push(/\.mjs$/);
        }
    });
    return config;
}
原因： file-loader、url-loader将.mjs解析成了base64字符串
