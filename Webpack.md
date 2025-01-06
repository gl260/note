# Webpack

```js
在vue.config.js配置webpack相关
module.exports = {
  // 开发服务器配置
  devServer: {},
  // 出口文件目录, 不能写在configureWebpack 会报错 (Avoid modifying webpack output.path directly. Use the "outputDir" option instead.避免直接修改webpack output.path。请改用“outputDir”选项。)
  outputDir: 'build',
  // webpack相关配置
  configureWebpack(config) {
    entry: '',
    plugins: [],
    config.externals = {},
  },
  // 第三方插件配置
  pluginOptions: {},
  chainWebpack(config){
    config.optimization.splitChunks({})
  },
} 
```

Vue CLI中configureWebpack与chainWebpack的区别?

* configureWebpack
  * 该对象将会被 webpack-merge 合并入最终的 webpack 配置
  * 当你需要简单地修改Webpack配置时，比如添加一些Loader或Plugin时,或者修改一些现有的配置项时,可以使用configureWebpack
  * 通过configureWebpack直接修改 Webpack 配置时，只能覆盖现有的配置，而不能对其进行细粒度的修改
* chainWebpack
  * 需要对 Webpack 配置进行更复杂的修改时，比如根据环境不同应用不同的配置，或者需要更精细地控制 Webpack 的配置时，可以使用chainWebpack

`configureWebpack` 与 `chainWebpack` 本质上没有什么区别,`configureWebpack`适用于简单的配置修改，而`chainWebpack`则更适用于复杂的修改



### devtool

* 控制是否生成, 以及如何生成source map

什么是source map?

* source map: 原代码映射
* source map能帮助我们在浏览器控制台上看到的错误时 能定位到错误在原代码的位置(能正确定位到原代码的行数)

| devtool属性         | 说明                                                         |
| ------------------- | :----------------------------------------------------------- |
| `(none)`            | 不设置的情况下默认为none - 不生成 source map，这是在生产环境是一个不错的选择 |
| `eval`              | 生成的代码和 source map 内容混淆在一起，通过eval输出, 主要缺点是，由于会映射到转换后的代码，而不是映射到原始代码，所以不能正确的显示行数。 |
| `source-map`        | 整个 source map 作为一个单独的文件生成，它为 bundle 添加了一个引用注释，以便开发工具知道在哪里可以找到它 |
| `eval-source-map`   | 每个模块使用 `eval()` 执行，并且 source map 转换为 DataUrl 后添加到 `eval()` 中。初始化 source map 时比较慢，但是会在重新构建时提供比较快的速度，并且生成实际的文件。行数能够正确映射，因为会映射到原始代码中。它会生成用于开发环境的最佳品质的 source map。 |
| `hidden-source-map` | 与 `source-map` 相同，但不会为 bundle 添加引用注释。如果你只想 source map 映射那些源自错误报告的错误堆栈跟踪信息，但不想为浏览器开发工具暴露你的 source map，这个选项会很有用。 |

#### 适合开发环境的配置 

* `eval` / `eval-source-map`
* mode设置为development时 devtool将被设置为eval

#### 适合生产环境的配置 

* `(none)` / `source-map` / `hidden-source-map`
* mode设置为production时 不为设置devtool 所以为(none)



### Mode

`mode` 配置选项，告知 webpack 使用相应模式的内置优化。

| 选项          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| `development` | 会将 `DefinePlugin` 中 `process.env.NODE_ENV` 的值设置为 `development`. |
| `production`  | 会将 `DefinePlugin` 中 `process.env.NODE_ENV` 的值设置为 `production` |
| `none`        | 不使用任何默认优化选项                                       |

如果没有设置，webpack 会给 `mode` 的默认值设置为 `production`



### devServer

#### open

* 告诉 dev-server 在服务器已经启动后打开浏览器。设置其为 `true` 以打开你的默认浏览器。

  ```js
  module.exports = {
    //...
    devServer: {
      open: true,
    },
  };
  ```

#### port

* 指定监听请求的端口号

* 要想自动使用一个可用端口请使用 `port: 'auto'`

  ```js
  module.exports = {
    //...
    devServer: {
      port: 8080,
    },
  };
  ```

#### proxy

* 代理后端开发服务器

  ```js
  module.exports = {
    //...
    devServer: {
      proxy: {
        '/api': 'http://192.168.1.1:3000',
      },
    },
  };
  // 现在，对 /api/users 的请求会将请求代理到 http://192.168.1.1:3000/api/users
  
  // 如果不希望传递/api，则需要重写路径：
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        pathRewrite: { '^/api': '' },
      },
    },
  },
    
  // 默认情况下，将不接受在 HTTPS 上运行且证书无效的后端服务器。 如果需要，可以这样修改配置
  devServer: {
    proxy: {
      '/api': {
        target: 'https://other-server.example.com',
        secure: false,
      },
    },
  },
  ```

* changeOrigin：它表示是否更新代理后请求的headers中host地址

#### host

- 指定要使用的 host。如果你想让你的服务器可以被外部访问

  ```js
  devServer: {
    host: '0.0.0.0',
  },
  ```

#### hot

* 启用 webpack 的 [模块热替换](https://webpack.docschina.org/concepts/hot-module-replacement/) 特性：

  ```js
  devServer: {
    hot: true,
  },
  ```

  

### 性能优化

* **打包后的结果**，上线时的性能优化。（比如分包处理、减小包体积、CDN服务器等）
* **优化打包速度**，开发或者构建时优化打包速度。（比如exclude、cache-loader等）

#### 代码分离

* 默认情况下，所有的JavaScript代码（业务代码、第三方依赖、暂时没有用到的模块）在首页全部都加载，就会影响首页 

  的加载速度

* 代码分离可以分出更小的bundle，以及控制资源加载优先级，提供代码的加载性能

* Webpack常用的代码分离有三种

  * 入口起点：使用entry配置手动分离代码
  * 防止重复：使用Entry Dependencies或者SplitChunksPlugin去重和分离代码
  * 动态导入：通过模块的内联函数调用来分离代码

**入口起点**

```js
// 入口起点, 就是配置多入口
entry: {
  index: './src/index.js',
  main: './src/main.js',
},
  
// 入口依赖
// 假如我们的index.js和main.js都依赖三个库：lodash、dayjs、axios
// 如果我们单纯的进行入口分离，那么打包后的两个bunlde都会有一份lodash、dayjs、axio
// 我们可以对他们进行共享
entry: {
  index: { import: './src/index.js', dependOn: 'aaa'}
  main: { import: './src/main.js', dependOn: 'aaa'},
  aaa: ['lodash', 'dayjs', 'axios']
},
```

**重复依赖**

```js
另外一种分包的模式是splitChunk, 底层是使用SplitChunksPlugin来实现的
该插件webpack已经默认安装和集成, 所以我们并不需要单独安装和直接使用该插件, 只需要提供SplitChunksPlugin相关的配置信息即可
// ...
optimization: {
  splitChunks: {
    // 将选择哪些 chunk 进行优化,默认值async,有效值'all','async','initial'
    // all会对同步和异步代码都进行处理
    // 默认值async 只会分割import()这种方式加载的模块成为一个单独的chunks, 而其他模块合并成为一个chunk。
    // initial
    chunks: 'async',
    minSize：30 * 1024, // 大于30kb的chunks就给分块, 如果一个包拆分出来达不到minSize,那么这个包就不会拆分
    minChunks: 1, // 表示一个模块至少应被minChunks个chunk所包含才能分割。默认为1
    minRemainingSize: 0, // 类似于minSize，最后确保提取的文件大小不能为0
    maxAsyncRequests: 10, // 按需加载时的最大并行请求数
    maxInitialRequests: 10, // 入口点的最大并行请求数
    // 超过50kb一定会打包, （minRemainingSize，maxAsyncRequests，maxInitialRequests）将被忽略。
    enforceSizeThreshold: 50 *1024, 
    maxSize: , // 将大于maxSize的包，拆分为不小于minSize的包
    // 定义缓存组，决定哪些模块会被打包到同一个代码块中。
    cacheGroups: {
      defaultVendors: {
        test: /[\\/]node_modules[\\/]/, // 匹配 node_modules 目录中的模块。
        priority: -10, // 缓存组的优先级，数值越大优先级越高。
        name: 'split', // 生成的代码块的名称。
        reuseExistingChunk: true, // 允许复用已经存在的代码块。
      },
      default: {
        minChunks: 2, // 模块被引用的最小次数，只有被引用次数大于等于这个值的模块才会被分割。
        priority: -20, // 缓存组的优先级，数值越大优先级越高。
        reuseExistingChunk: true, // 允许复用已经存在的代码块。
      },
      libs: {
        name: 'chunk-libs',
        test: /[\\/]node_modules[\\/]/, // 匹配 node_modules 目录中的模块。
        priority: 10, // 优先级，数值越大优先级越高。
        chunks: 'initial', // 只打包最初依赖的第三方库。
      },
      components: {
        chunks: 'all', // 分割所有类型的代码。
        test: /[\\/]src[\\/]components[\\/]/, // 匹配 src/components 目录中的模块。
        priority: 21, // 优先级，数值越大优先级越高。
        name: 'chunk-components', // 生成的代码块的名称。
      },
    }
  }
}
```

**动态导入**

```js
// 动态import使用最多的一个场景是懒加载(路由懒加载)
{
  path: '/',
  name: '首页',
  component: () => import(/* webpackChunkName: "home" */ '@/views/index'),
},
```

#### runtimeChunk

* 配置runtime相关的代码是否抽取到一个单独的chunk中

  * runtime相关的代码指的是在运行环境中，对模块进行解析、加载、模块信息相关的代码

  * 比如我们的component、bar两个通过import函数相关的代码加载，就是通过runtime代码完成的

* 抽离出来后，有利于浏览器缓存的策略

  * 比如我们修改了业务代码（main），那么runtime和component、bar的chunk是不需要重新加载的
  * 比如我们修改了component、bar的代码，那么main中的代码是不需要重新加载的

```js
optimization: {
  // ...
  runtimeChunk: {
    name: 'runtime',
  },
}
```

#### Prefetch/Preload

* 在声明 import 时，使用下面这些内置指令，来告知浏览器\
  * prefetch(预获取)：将来某些导航下可能需要的资源 
  * preload(预加载)：当前导航下可能需要资源

```js
{
  path: '/',
  name: '首页',
  component: () => import(/* webpackChunkName: "home" */ /* webpackPreload: true */ '@/views/index'),
},
```

* 与 prefetch 指令相比，preload 指令有许多不同之处：*
  * preload chunk 会在父 chunk 加载时，以并行方式开始加载。prefetch chunk 会在父 chunk 加载结束后开始加载。
  * preload chunk 具有中等优先级，并立即下载。prefetch chunk 在浏览器闲置时下载。 
  * preload chunk 会在父 chunk 中立即请求，用于当下时刻。prefetch chunk 会用于未来的某个时刻。

#### DNS

externals

* **防止**将某些 `import` 的包(package)**打包**到 bundle 中，而是在运行时(runtime)再去从外部获取这些扩展依赖
* 例如，从 CDN 引入Vue VueX axios vue-router，而不是把它打包：

```js
const isProd = process.env.NODE_ENV === 'production';
module.exports = {
  //...
  configureWebpack(config) {
    if (isProd) {
      config.externals = {
        axios: 'axios',
        vue: 'Vue',
        vuex: 'Vuex',
        'vue-router': 'VueRouter',
      } 
    }
  },
  chainWebpack(config){
    config.plugin('html').tap(args => {
      if(isProd){
        args[0].title = '修改标题',
        args[0].cdn = {
          css: [],
          js: [
            'https://axios链接',
            'https://Vue链接',
            'https://Vuex链接',
            'https://VueRouter链接',
          ]
        }
      }
      return args
    })
  },
};
```

#### MiniCssExtractPlugin

* 会将 CSS 提取到单独的文件中，为每个包含 CSS 的 JS 文件创建一个 CSS 文件，并且支持 CSS 和 SourceMaps 的按需加载
* 安装 mini-css-extract-plugin
  * `npm install --save-dev mini-css-extract-plugin`
* 建议 `mini-css-extract-plugin` 与 `css-loader` 一起使用。之后将 loader 与 plugin 添加到你的 `webpack` 配置文件中

```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
module.exports = {
  plugins: [new MiniCssExtractPlugin()],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
      },
    ],
  },
};
```























































