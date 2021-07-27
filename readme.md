# Entry
設定程式進入點

# Output
設定程式輸出資料夾與檔名

# Mode
分為`development`、`production`、`none`  
在`development`模式下，程式不會被壓縮。`production`模式下則會

# Loaders (module)
設定載入除了JS之外的檔案時，要遵照的規則，如CSS、圖片等等，通常會需要另外安裝相對應的loader套件

# Plugins
設定除了loader之外的轉換，如程式碼最佳化、自動化調整環境變數等等

# Plugins 功能介紹

## [HtmlWebpackPlugin](https://webpack.js.org/plugins/html-webpack-plugin/#root)
能夠設定產生的HTML，如引入JS與CSS的hash值、參考產生的HTML內容等，  
設定可以寫在
```
plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html"
    })
]
```

## [MiniCssExtractPlugin](https://webpack.js.org/plugins/mini-css-extract-plugin/#root)
能夠切開產生的CSS檔案，沒有使用此套件的時候，會在產生的JS中寫入CSS。使用此套件後會獨立產生一個CSS檔案，  
檔名與其他設定可以寫在
```
plugins: [
    new MiniCssExtractPlugin({
        filename: "main.[hash].css"
    })
]
```

## [Clean plugin for webpack](https://github.com/johnagan/clean-webpack-plugin)
build時，自動清除output files

## [copy-webpack-plugin](https://github.com/webpack-contrib/copy-webpack-plugin)
build時，自動將指令目錄複製至output目錄

## [CompressionWebpackPlugin](https://webpack.js.org/plugins/compression-webpack-plugin/)
build時，自動建立打包後的壓縮檔

## [DefinePlugin](https://webpack.js.org/plugins/define-plugin/)
compile時，會依據config中的設定建立全域變數。若有不同環境的config可以使用

# [devtool](https://webpack.js.org/configuration/devtool/#root)
內建各種模式可以產生不同的source map

# [Asset Modules](https://webpack.js.org/guides/asset-modules/#root)
webpack內建的loader，以載入圖片來說，在rules中加入
```
{
    test: /\.png/,
    type: 'asset/resource'
}
```

# [PostCSS](https://github.com/postcss/postcss)
會根據安裝的插件調整CSS的內容，如加入各瀏覽器的prefix等等

1. 安裝
```
npm install postcss -D
npm install postcss-loader -D
```

2. 建立 `postcss.config.js` 並加入
```
module.exports = {
  plugins: [require("autoprefixer")]
};
```

3. 建立相對應的browserslist
```
"browserslist": [
    "last 2 versions"
]
```  

# [Babel](https://babeljs.io/)
1. 安裝
```
npm install babel-loader @babel/core @babel/preset-env -D
```

2. rules加入
```
{
    test: /\.m?js$/,
    exclude: /node_modules/,
    use: {
        loader: "babel-loader",
        options: {
        presets: ['@babel/preset-env']
        }
    }
}
```      

3. 可以加入 `babel.config.json` 做設定，如
```
// babel.config.json
{
  "presets": ["@babel/preset-env"]
}
```  

