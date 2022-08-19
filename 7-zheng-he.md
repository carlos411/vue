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



## 載入圖片



在 script 當中使用：

```javascript
import logo from './assets/vue.svg';
console.log(logo);

const logo = new URL("./assets/vue.svg", import.meta.url).href;
console.log(logo);
```



在 template 當中使用：

```html
<!-- 絕對路徑，在 public 資料夾下 -->
<img src="/vite.svg">
<!-- 相對路徑 -->
<img src="./assets/vue.svg">

<!-- 使用變數 logo -->
<img :src="logo">
```



## 載入 JSON 檔

假設 `src/data.json` 內容如下：

```javascript
{
  "framework": "Vue",
  "buildTool": "Vite, of course!",
  "developerMood": "Happy."
}
```

在 `src/App.vue` 的 script 當中使用：

```javascript
import data from './data.json';
console.log(data);

// 以下這個，在 npm run build 之後，只會載入需要的，效能較好
import { developerMood } from './data.json';
console.log(developerMood);
```



## 自動載入

自動載入 `src/autoImports` 資料夾裡的所有 JS 檔，以下提供兩個方式：

```javascript
/*
// 非同步方式
const autoImportedModules = import.meta.glob("./autoImports/*.js");
console.log(autoImportedModules);
for(const path in autoImportedModules){
  autoImportedModules[path]();
}
*/


// 同步方式
// const autoImportedModules = import.meta.globEager("./autoImports/*.js");
```



## 環境變數與模式

使用 **`import.meta.env`**。

在根資料夾下，建立 **`.env`** 檔案，內容如下：

如果是以 **`VITE_`** 做開頭的，就會被放入 **`import.meta.env`** 物件當中：

```
VITE_MY_HEADLESS_CMS_PUBLIC_KEY=123
VITE_MY_HEADLESS_CMS_URL=https://mycms.com
```

模式可透過以下指令來改變( **`import.meta.env`** 裡的 mode 就會改變 )：

```bash
$ npm run build -- --mode-staging
```



## dev 與 build 與 preview

啟動開發用的伺服器：

```bash
$ npm run dev
```

build：

```bash
$ npm run build
$ npm run build -- --mode=staging
```



瀏覽 build 之後的頁面：

```bash
$ npm run preview
```

