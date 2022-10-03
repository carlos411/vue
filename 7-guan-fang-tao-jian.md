# 7 單頁式應用程式(SPA)

SPA: Single Page Application

在專案開始前，就需要先決定是否要導入此架構，而不是網站做到一半才導入。



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

