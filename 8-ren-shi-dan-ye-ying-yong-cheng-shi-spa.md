# 8 認識單頁應用程式(SPA)

SPA: Single Page Application

在專案開始前，就需要先決定是否要導入此架構，而不是網站做到一半才導入。做 SPA 主要需要三個工具：

* [Vite](https://vitejs.dev/)
* [Vue](https://vuejs.org/)
* [Vue Router](https://router.vuejs.org/)



註：安裝 Vite 之前，官方有[以下的敘述](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)：

<figure><img src=".gitbook/assets/vite_nodejs_support.png" alt=""><figcaption></figcaption></figure>

也就是需先安裝 [Node.js](https://nodejs.org/en/) 14.18 以上的版本。可執行以下指令(**`node -v`**)查看 Node.js 目前您電腦所使用的版本(以下的 **`$`** 代表是指令的意思，所以請勿輸入錢字號)：

```bash
$ node -v
v18.12.1
```

若 Node.js 未安裝，如下圖下載安裝：

<figure><img src=".gitbook/assets/nodejs_install_hint.png" alt=""><figcaption></figcaption></figure>



## 第 1 步：安裝 Vite

假設在電腦桌面建立 vite 資料夾，就在 vite 資料夾下，執行以下指令：

```bash
npm create vite@latest
```



```
Project name: spa-app
Select a framework: Vue
Select a variant: JavaScript
```

再執行以下指令：

```
cd spa-app
npm install
npm run dev
```

看到如下圖：

<figure><img src=".gitbook/assets/vite_npm_run_dev.png" alt=""><figcaption></figcaption></figure>



將 **`components/HelloWorld.vue`** 檔的 script 標籤都註解起來，改成以下：

{% code lineNumbers="true" %}
```html
<!--
<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>
-->
<script>
export default {
  props: ["msg"],
  data(){
    return {
      count: 0
    }
  }
}
</script>
```
{% endcode %}



## 第 2 步：認識資料夾及 build 和 preview

打包產生 **`dist`** 資料夾(如果最後要上線，要上線的是 dist 資料夾裡的東西)：

```bash
npm run build
```



瀏覽 **`dist`** 資料夾：

```
npm run preview
```

出現如下圖：

<figure><img src=".gitbook/assets/npm_run_preview.png" alt=""><figcaption></figcaption></figure>



## 第 3 步：安裝 Vue Router

```bash
npm install vue-router@4
```

此時，在 **`package.json`** 檔，會多了以下 **`vue-router`** 的部份：

{% code lineNumbers="true" %}
```javascript
"dependencies": {
    ...
    "vue-router": "^4.1.6"
    
  },
```
{% endcode %}



## 第 4 步：設定 `@` 指向到 src 資料夾

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

關於 `vite.config.js` 的相關設定，可參考官方：[https://vitejs.dev/config/](https://vitejs.dev/config/)

針對 `resolve.alias` 的部份，可參考：[https://vitejs.dev/config/shared-options.html#resolve-alias](https://vitejs.dev/config/shared-options.html#resolve-alias)



## 第 5 步：放圖檔

建立 `src/assets/images/` 資料夾，放入以下三張圖檔(直接下載)：

[https://alldata.sgp1.digitaloceanspaces.com/images/vue\_images.zip](https://alldata.sgp1.digitaloceanspaces.com/images/vue\_images.zip)





## 第 6 步：認識 vue 檔

將 **`style.css`** 檔的內容全部移除，改成如下：

{% code lineNumbers="true" %}
```css
* {
  box-sizing: border-box;
}
body{
  margin: 0;
}
/* 設定圖片最大寬度為 100% */
img {
  max-width: 100%;
}

footer.footer {
  text-align: center;
  font-size: 0.8rem;
  color: #999;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #ccc;
}
```
{% endcode %}

將 **`App.vue`** 檔，更新成如下：

{% code lineNumbers="true" %}
```html
<script>
</script>

<template>
</template>

<!-- 這裡的 scoped 屬性，是讓所寫的 CSS，「只」會套用到此元件的 template。 -->
<style scoped>
</style>
```
{% endcode %}

將 components 資料夾裡的 **`HelloWorld.vue`** 檔案移除。(若想保留當參考，可不用移除。)



## 第 7 步：建立首頁(Intro)

* 建立 **`src/views/`** 資料夾：「`每個頁面(view)`」都會對應到一個「`vue 元件檔`」。
* 建立 **`src/router/`** 資料夾：用來管理`網址(路由)`。



建立首頁會用到的 **`src/views/Intro.vue`** 元件檔。

以及 **`src/router/index.js`** 路由檔。

然後更新以下原始碼，如下：

{% tabs %}
{% tab title="src/router/index.js" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">import { createRouter, createWebHistory } from "vue-router";

const routes = [
  // 網址定義：/；給定名稱 Home；載入 Home.vue 元件
  {path: '/', name: 'Home', component: () => import('@/views/Intro.vue')}
];

<strong>const router = createRouter({
</strong>  history: createWebHistory(),
  routes
});

export default router;
</code></pre>
{% endtab %}

{% tab title="src/views/Intro.vue" %}
{% code lineNumbers="true" %}
```javascript
<script>
  export default {
    data(){
      return {
      };
    }
  }
</script>

<template>
  <div class="intro">
      
      <div class="intro__item">
        <div class="intro__item__img">
          <img src="@/assets/images/1_640x360.jpg">
        </div>
        <div class="intro__item__text">
          <h2 class="title2">Kindle</h2>
          <p class="para">
            Kindle 是一款電子書閱讀器，由美國亞馬遜公司開發，於2007年11月19日推出。Kindle的名字來自於亞馬遜公司的網站名稱，亞馬遜公司的網站名稱是以亞馬遜河的名字命名的，而亞馬遜河的名字來自於一個古希臘語的詞，意思是「沒有尾巴的河」，而Kindle的名字也是以此為由。
          </p>
        </div>
      </div>

      <div class="intro__item">
        <div class="intro__item__text">
          <h2 class="title2">風景</h2>
          
          <p class="para">
            綠色的海邊，橘黃色的沙灘，藍色的海，藍色的天空，白色的雲，這些都是海邊的風景。海邊的風景很漂亮，我們可以在海邊玩耍，也可以在海邊看日出日落。
          </p>

        </div>
        <div class="intro__item__img">
          <img src="@/assets/images/2_640x360.jpg">
        </div>
      </div>

      <div class="intro__item">
        <div class="intro__item__img">
          <img src="@/assets/images/3_640x360.jpg">
        </div>
        <div class="intro__item__text">
          <h2 class="title2">第三個區塊</h2>
          <p class="para">
            貓咪是一種可愛的動物，我們可以養貓，也可以養狗。貓咪的毛很柔軟，我們可以摸摸它的毛，也可以摸摸它的肚子。
          </p>
        </div>
      </div>

    </div>
</template>

<style scoped>
/* div.intro__item 裡的內容橫向排列 */
div.intro__item {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  /* 設定寬度，讓內容置中 */
  width: 100%;
  /* 設定上下間距 */
  margin: 1rem 0;
  /* 顯示邊框 */
  border: 1px solid #ccc;
}
/* 左右兩個區塊寬度設定一樣 */
div.intro__item > div {
  width: 50%;
  /* 不要有縫隙 */
  padding: 0;
}
/* div.intro__item__img 想要放在上面，使用 align-self */
div.intro__item__img {
  align-self: flex-start;
}
/* div.div.intro__item__img 裡的圖片佔滿父元素 */
div.intro__item__img > img {
  width: 100%;
}

/* 圖片的下方不要有縫隙 */
div.intro__item > div.intro__item__img > img {
  vertical-align: bottom;
}
/* div.intro__item__img 奇數列跟旁邊的文字設定一點間距 */
div.intro__item__img:nth-child(odd) {
  margin-right: 1rem;
}
/* div.intro__item__img 偶數列跟旁邊的文字設定一點間距 */
div.intro__item__img:nth-child(even) {
  margin-left: 1rem;
}
/* 將 h2.title2 優化一下外觀 */
h2.title2 {
  font-size: 1.2rem;
  color: #333;
  /* 設定上下間距 */
  margin: 0.5rem .5rem;
}
/* 將 p.para 優化一下外觀 */
p.para {
  font-size: 0.9rem;
  color: #666;
  /* 設定上下間距 */
  margin: 0.5rem 0.5rem;
}

/* 在螢幕寬度小於等於 575.98px時，將 div.intro__item__img 放在 div.intro__item__text 的上方 */
@media (max-width: 575.98px) {
  /* 將 div.intro__item 裡的內容設定上下排 */
  div.intro__item {
    flex-direction: column;
  }
  div.intro__item__img {
    order: 1;
    /* 寬度 100% */
    width: 100% !important;
    /* 移除 margin 和 padding */
    margin: 0 !important;
    padding: 0;
  }
  /* div.intro__item__img 裡的圖片寬度直接佔滿父元素 */
  div.intro__item__img > img {
    width: 100%;
  }
  div.intro__item__text {
    order: 2;
    /* 寬度 100% */
    width: 100% !important;
  }
  /* div.div.intro__item__text 裡面的 h2 和 p 給點內距 */
  div.intro__item__text > h2, div.intro__item__text > p {
    padding: 0 1rem;

    /* 左邊的 margin 設定 0 */
    margin-left: 0;
    /* 右邊也是 */
    margin-right: 0;

  }
}
</style>

```
{% endcode %}
{% endtab %}

{% tab title="src/main.js" %}
{% code lineNumbers="true" %}
```javascript
import { createApp } from 'vue'
//import './style.css'
import App from './App.vue'
import router from '@/router/index.js'

createApp(App).use(router).mount('#app');
```
{% endcode %}
{% endtab %}

{% tab title="src/App.vue" %}
{% code lineNumbers="true" %}
```javascript
<script>
  export default {
    data(){
      return {};
    }
  }
</script>

<template>
  <router-view v-slot="{Component}">
    <component :is="Component" :key="$route.path"></component>
  </router-view>
</template>

<style scoped>
</style>
```
{% endcode %}
{% endtab %}
{% endtabs %}



在編輯 Home.vue 時，若出現以下的訊息：

<figure><img src=".gitbook/assets/volar_hint_1.png" alt=""><figcaption></figcaption></figure>

可透過下圖來關掉提示(先進到編輯器的偏好設定)：

<figure><img src=".gitbook/assets/volar_hint_2.png" alt=""><figcaption></figcaption></figure>





## 第 7 步：建立第二個頁面

更新以下程式：

{% tabs %}
{% tab title="src/router/index.js" %}
在 routes 陣列當中，多加一個：

{% code lineNumbers="true" %}
```javascript
{path: '/destination/:id', name: 'destination', component: () => import('@/views/Destination.vue')}
```
{% endcode %}
{% endtab %}

{% tab title="src/views/Destination.vue" %}
{% code lineNumbers="true" %}
```javascript
<script>
  export default {
    data(){
      return {
        name: "臺北"
      };
    }
  }
</script>

<template>
  <div class="block">
    目的地：{{ name }}
  </div>
</template>

<style scoped>
</style>
```
{% endcode %}
{% endtab %}
{% endtabs %}





## 第 8 步：加上導覽列

更新 **`src/App.vue`**，在 template 標籤當中，加以下的原始碼：

{% code lineNumbers="true" %}
```html
<header>
  <a href="/">首頁</a> |
  <a href="/destination/1">臺北</a> |
  <a href="/destination/2">桃園</a>
</header>
```
{% endcode %}

然後測一下(觀察開發者工具的 network)，測完之後，改成用以下：

{% code lineNumbers="true" %}
```html
<header>
  <router-link to="/">首頁</router-link> |
  <router-link to="/destination/1">臺北</router-link> |
  <router-link to="/destination/2">桃園</router-link>
</header>
```
{% endcode %}



## 第 9 步：加上資料

加上 **`src/data.json`**，內容如下：

{% code lineNumbers="true" %}
```json
{
  "destinations": [
    {
      "name": "臺北",
      "id": 1,
      "description":"臺北景點描述"
    },
    {
      "name": "桃園",
      "id": 2,
      "description":"桃園景點描述"
    }
  ]
}
```
{% endcode %}



## 第 10 步：加上迴圈跑導覽列

更新 **`src/App.vue`**，script 標籤的部份，內容如下：

{% code lineNumbers="true" %}
```javascript
<script>
  import sourceData from "@/data.json";

  export default {
    data(){
      return {
        destinations: sourceData.destinations
      };
    }
  }
</script>
```
{% endcode %}



header 標籤的部份，改成如下：

{% code lineNumbers="true" %}
```html
<header>
  <router-link to="/">首頁</router-link> |
  <router-link v-for="destination in destinations" :key="destination.id" :to="'/destination/'+destination.id">
    {{ destination.name }}
  </router-link>
  <!-- <router-link to="/destination/1">臺北</router-link> | -->
  <!-- <router-link to="/destination/2">桃園</router-link> -->
</header>
```
{% endcode %}



## 第 11 步：景點頁面修改

修改 **`views/Destination.vue`** 頁面：

{% code lineNumbers="true" %}
```javascript
<script>
  import sourceData from "@/data.json";

  export default {
    data(){
      return {
        //name: "臺北"
      };
    },
    computed: {
      // destination(){
      //   var d = sourceData.destinations.find((destination) => {
      //     return destination.id == parseInt(this.$route.params.id)
      //   });
      //   return d;
      // },
      destination(){
        return sourceData.destinations.find(destination => destination.id == parseInt(this.$route.params.id));
      }
    }
  }
</script>

<template>
  <div class="block">
    目的地：{{ destination.name }}
    <br>
    {{ destination.description }}

  </div>
</template>

<style scoped>
</style>
```
{% endcode %}



## 第 12 步：建立導覽列元件

建立 **`src/components/TheNavigation.vue`** 檔案，內容如下：

{% code lineNumbers="true" %}
```javascript
<script>
  import sourceData from "@/data.json";
  export default {
    data(){
      return {
        destinations: sourceData.destinations
      };
    }
  }
</script>

<template>
  <router-link v-for="destination in destinations" :key="destination.id" :to="'/destination/'+destination.id">
    {{ destination.name }}
  </router-link>
</template>

<style scoped>
</style>
```
{% endcode %}



更新 **`src/App.vue`**，內容如下：

{% code lineNumbers="true" %}
```javascript
<script>
  //import sourceData from "@/data.json";
  import TheNavigation from "@/components/TheNavigation.vue";

  export default {
    components: {TheNavigation},
    data(){
      return {
        //destinations: sourceData.destinations
      };
    }
  }
</script>

<template>
  <header>
    <router-link to="/">首頁</router-link> |
    
    <TheNavigation></TheNavigation>
    
    <!-- <router-link v-for="destination in destinations" :key="destination.id" :to="'/destination/'+destination.id">
      {{ destination.name }}
    </router-link> -->
    <!-- <router-link to="/destination/1">臺北</router-link> | -->
    <!-- <router-link to="/destination/2">桃園</router-link> -->
  </header>

  <router-view v-slot="{Component}">
    <component :is="Component" :key="$route.path"></component>
  </router-view>
</template>

<style scoped>
</style>
```
{% endcode %}



## 第 13 步：載入外部 CSS

建立 **`public/main.css`** 檔案：

{% code lineNumbers="true" %}
```css
* {
  box-sizing: border-box;
}
body{
  margin: 0;
}
#app header{
  background-color: #2c3e50;
}

#app header a{
  color: white;
  display: inline-block;
  margin-right: 20px;
}

#app div.block{
  background-color: #ddd;
  height: 200px;
}
```
{% endcode %}

在 **`index.html`** 檔的 head 結束標籤之前，放以下原始碼：

{% code lineNumbers="true" %}
```html
<link rel="stylesheet" href="/main.css">
```
{% endcode %}



## 第 14 步：build and preview

產生 dist 資料夾：

```
npm run build
```

瀏覽 dist 資料夾：

```
npm run preview
```

如果未來要上線，要上線的會是 **`dist`** 資料夾。



## 第 15 步：建立另一個網頁檔

在 **`spa-app`** 資料夾下，建立 **`index2.html`**，內容如下：

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <h1>另一個頁面</h1>
  </body>
</html>
```
{% endcode %}

如果使用 **`npm run build`** 指令的話，是不會有 `index2.html` 檔案的，要再加以下的設定才會有。



更新 **`vite.config.js`**，內容如下(多 **`build`** 那個部份)：

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
  },
  build: {
    rollupOptions: {
      input: {
        main: path.resolve(__dirname, 'index.html'),
        other: path.resolve(__dirname, 'index2.html')
      }
    }
  }
})
```
{% endcode %}

若需要 build 的話，就再執行：

```
npm run build
npm run preview
```



## 第 16 步：放 YouTube 影片來認識 SPA

更新 **`src/App.vue`** 檔案，在 **`router-view`** 標籤 **同層的下方** 或 **裡面**，加以下的原始碼：

{% code lineNumbers="true" %}
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/STWVMl_cGuc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
{% endcode %}



然後可再試試 **`router-link`** 與一般 **`a`** 標籤的差別。



## 完成的範例

[https://alldata.sgp1.digitaloceanspaces.com/sample/spa-app.zip](https://alldata.sgp1.digitaloceanspaces.com/sample/spa-app.zip)

需記得在 **`spa-app`** 資料夾下，執行以下指令來安裝相關套件(即產生 `node_modules` 資料夾)：

```bash
npm install
```





