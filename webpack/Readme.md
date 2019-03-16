# webpack





## webpack 

### 一、简介

###	 *webpack* 是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler)*。当 webpack 处理应用程序时，它会递归地构建一个*依赖关系图(dependency graph)*，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 *bundle*。



### 二、 使用步骤

#### 1、安装webpack

> 全局安装webpack
>
> ```shell
> npm install webpack -g
> ```
>
> 开发环境下安装webpack
>
> ```shell
> npm install webpack --save--dev
> ```
>
> - **-save-dev与-save的区别**
>
>   > npm install在安装node模块时，有两种命令参数可以把它们的信息写入package.json文件：
>   >
>   > ```shell
>   > -save
>   > -save-dev
>   > ```
>   >
>   > –save会把依赖包名称添加到package.json文件dependencies键下，–save-dev则添加到package.json文件devDependencies键下,例如：
>   >
>   > ```json
>   > {
>   >     "name": "yo",
>   >     "version": "0.0.0",
>   >     "dependencies": {},
>   >     "devDependencies": {
>   >         "grunt": "~0.4.1",
>   >         "grunt-contrib-copy": "~0.4.1",
>   >         "grunt-contrib-concat": "~0.3.0",
>   >         "grunt-contrib-uglify": "~0.2.0",
>   >         "grunt-contrib-compass": "~0.7.0",
>   >         "grunt-contrib-jshint": "~0.7.0",
>   >         "grunt-contrib-cssmin": "~0.7.0",
>   >     }
>   > }
>   > ```
>   >
>   > dependencies与devDependencies的区别：devDependencies下列出的模块，是我们开发时用的依赖项，像一些进行单元测试之类的包，比如grunt-contrib-uglify，我们用它混淆js文件，它们不会被部署到生产环境。dependencies下的模块，则是我们生产环境中需要的依赖，即正常运行该包时所需要的依赖项。
>   >
>   > 如果你将包下载下来在包的根目录里运行,执行如下命令,默认会安装两种依赖:
>   >
>   > ```shell
>   > npm install
>   > ```
>   >
>   > 如果你只是单纯的使用这个包而不需要进行一些改动测试之类的，只安装dependencies而不安装devDependencies。执行：
>   >
>   > ```shell
>   > npm install --production
>   > ```
>   >
>   > 通过“npm install packagename”进行安装，只会安装dependencies:
>   >
>   > ```shell
>   > npm install packagename
>   > ```
>   >
>   > 如需安装devDependencies，执行：
>   >
>   > ```shell
>   > npm install packagename --dev  
>   > ```
>   >
>   > 总结：`webpack`，`gulp`等打包工具，这些都是我们开发阶段使用的，代码提交线上时，不需要这些工具，所以我们将它放入`devDependencies`即可，但是像`jquery`这类插件库，如果我们不把他打入线上代码中，那么项目就可能报错，无法运行，所以类似这种项目必须依赖的插件库，我们则必须打入`dependencies`中
>   >
>   > 



#### 2、使用

+ 命令行中使用

  ```shell
  webpack 入口文件 -o 输出文件
  ```

  实例:

  ```shell
  webpack .\src\main.js -o .\dist\bundle.js
  ```

  通过配置文件 `webpack.config.js` 简化命令行中使用:

  ```javascript
  const path = require('path')
  
  module.exports = {
      // 入口文件
      entry: path.join(__dirname, 'src/main.js'),  
      
      // 输出文件
      output: {
          path: path.join(__dirname, 'dist'),  
          filename: 'bundle.js'
      }
  }
  ```

  配置后在命令行执行 `webpack `命令即可，与 `webpack .\src\main.js -o .\dist\bundle.js`同样效果

  

  

  ## webpack-dev-server

  ### 一、简介

  使用 `webpack-dev-server`实现自动打包编译的功能，类似于 nodemon.js

  ### 一、使用方法

  + 1、 运行 `npm i webpack-dev-server -D` 来把这个工具安装到项目的本地开发依赖

  + 2、安装完毕后和 `webpack` 命令用法完全一样，如果在项目本地安装的`webpack-dev-server` 而不是在全局 `-g`安装 ，无法当做脚本命令直接在 `powershell`终端中直接运行；只有安装到全局`-g`的工具，才能在终端中正常执行，解决方法可以在`package.json`文件下的`script`对象中添加,例如：

    ```shell
    "scripts": {
        "dev": "webpack-dev-server"
    }
    ```

    然后通过 `npm run dev`运行该命令

  + 3、要使用`webpack-dev-server`必须安装`webpack`

  + 4、`webpack-dev-server`打包生成的 bundle.js 文件，并未存放到实际的物理磁盘中，而是直接托管到了内存中，所有在项目根目录中找不到这个导报好的 bundle.js 文件

  + 5、`webpack-dev-server`把打包好的文件，以一种虚拟的形式，托管到了项目根目录中，可以认为和 `dist src node_modules` 平级有一个看不见的文件，叫做 bundile.js

    

  

  

  

  

  

  

  

