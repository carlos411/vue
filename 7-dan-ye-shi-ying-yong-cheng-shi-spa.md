# 7 單頁式應用程式(SPA)

SPA: Single Page Application

在專案開始前，就需要先決定是否要導入此架構，而不是網站做到一半才導入。靠兩個工具：

* [Vite](https://vitejs.dev/)
* [Vue Router](https://router.vuejs.org/)



註：安裝 vite 之前，需安裝 Node.js 14.18 以上的版本。可執行以下指令查看 Node.js 的版本：

```bash
node -v
```

## 第 1 步：安裝 Vite

在特定資料夾下，執行指令：

```bash
npm create vite@latest
```



```
Project name: travel-app
Select a framework: Vue
Select a variant: JavaScript

cd travel-app
npm install
npm run dev
```



## 第 2 步：認識資料夾及 build 和 preview

打包產生 dist 資料夾：

```bash
npm run build
```

瀏覽 dist 資料夾：

```
npm run preview
```



## 第 3 步：安裝 Vue Router

```bash
npm install vue-router@4 --save
```



## 第 4 步：設定指向到 src 資料夾

更新 **`vite.config.js`** 檔案。

設定別名 **`@`** 指向到 **`src`** 資料夾：

新增第3行及第8行的 resolve：

{% code lineNumbers="true" %}
```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src")
    }
  }
})

```
{% endcode %}



## 第 5 步：認識 vue 檔

將 **`style.css`** 檔的內容全部移除。

將 **`App.vue`** 檔，更新成如下：

{% code lineNumbers="true" %}
```javascript
<script>
</script>

<template>
</template>

<style scoped>
</style>
```
{% endcode %}



## 第 6 步：建立首頁

建立首頁會用到的 **`components/Home.vue`** 元件檔。

以及 **`router/index.js`** 路由檔，及其它更新。

內容如下：





