# Webpack

### devtool

* 控制是否生成, 以及如何生成source map

什么是source map?

* source map: 原代码映射
* source map能帮助我们在浏览器控制台上看到的错误时 能定位到错误在原代码的位置

| devtool属性         | 说明                                                         |
| ------------------- | :----------------------------------------------------------- |
| `(none)`            | 不设置的情况下默认为none - 不生成 source map，这是在生产环境是一个不错的选择 |
| `eval`              | 生成的代码和 source map 内容混淆在一起，通过eval输出, 主要缺点是，由于会映射到转换后的代码，而不是映射到原始代码，所以不能正确的显示行数。 |
| `source-1map`       | 整个 source map 作为一个单独的文件生成，它为 bundle 添加了一个引用注释，以便开发工具知道在哪里可以找到它 |
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

















