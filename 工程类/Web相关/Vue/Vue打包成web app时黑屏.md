# Vue打包成web app时黑屏

**解决方法：**

**1. vue-cli 2.x版本**

 在config文件夹下的index.js中修改 assetsPublicPath: './'

**2. vue-cli 3.x版本**

在 cli3 中 assetsPublicPath 属性被 baseUrl 取代，只需要在vue.config.js 添加baseUrl 属性 设为 ‘./’ 即可

![img](https://img2020.cnblogs.com/blog/1353328/202005/1353328-20200520103414200-492003257.png)

**3. vue-cli 4.x版本**

与cli3相同都是修改 vue.config.js 文件 ，但将属性换为  publicPath:'./' 

![img](https://img2020.cnblogs.com/blog/1353328/202005/1353328-20200520103654443-1652492734.png)