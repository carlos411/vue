# 7 整合

* [Vue](https://vuejs.org/)：介面元件。
* [Vite](https://vitejs.dev/)：Server、Build、HMR。
* [Vue Router](https://router.vuejs.org/)：SPA。

## 安裝

進到自己指定的資料夾，然後執行：

```bash
$ npm init vite@latest
```

然後會要輸入「專案資料夾」的名稱(也可直接按 enter 使用預設的 `vite-project`)，然後 framework 選擇 vue ，然後 variant 再選擇 vue 即可。然後執行以下：

```bash
$ cd vite-project
$ npm install
```



## 啟動網站

```bash
$ npm run dev
```



## 使用 CSS 或 SASS 或 PostCSS

除了在 css 檔中可以使用 @import 語法之外，也可以使用以下：



以 `App.vue` 為例：

```javascript
<script setup>
  import './assets/main.css'
</script>

<style>
  @import "./assets/main.css" (max-width: 800px);
</style>
```

以 `main.js` 為例：

```javascript
import './assets/main.css'
```



如果要使用 sass 語法，需先安裝：

```bash
$ npm install --save-dev sass
```

然後只要將 main.css 的檔名，改成 main.scss 或 main.sass，然後載入即可。



以及如果要在元件當中的 style 標籤使用 scss 或 sass 語法的話，可使用以下：

```html
<style lang="sass">
</style>
```

或

```html
<style lang="scss">
</style>
```



註：如果要移除 sass，就執行以下指令：

```bash
$ npm uninstall sass
```



如果要使用 PostCSS 的巢狀功能，就安裝：

```bash
$ npm install --save-dev postcss-nesting
```

然後建立 `postcss.config.js` 檔案，內容如下：

```javascript
export default {
  plugins: {
    "postcss-nesting": {}
  }
}
```

