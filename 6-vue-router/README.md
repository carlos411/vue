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



## 使用 CSS 及 SASS

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

