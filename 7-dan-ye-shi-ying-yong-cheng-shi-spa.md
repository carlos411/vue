# 7 簡介：單頁應用程式(SPA)

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

建立首頁會用到的 **`src/views/Home.vue`** 元件檔。

以及 **`src/router/index.js`** 路由檔，及其它更新。

內容如下：

{% tabs %}
{% tab title="src/router/index.js" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">import { createRouter, createWebHistory } from "vue-router";

const routes = [
  {path: '/', name: 'Home', component: Home}
];

<strong>const router = createRouter({
</strong>  history: createWebHistory(),
  routes
});

export default router;</code></pre>
{% endtab %}

{% tab title="src/views/Home.vue" %}
{% code lineNumbers="true" %}
```javascript
<script>
  export default {
    data(){
      return {
        msg: "Home"
      };
    }
  }
</script>

<template>
  <div class="block">
    這是：{{ msg }}
  </div>
</template>

<style scoped>
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

{% tab title="Untitled" %}
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
  <div>
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

修改 **`views/destination.vue`** 頁面：

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
  <div>
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



## 第 13 步：build and preview

產生 dist 資料夾：

```
npm run build
```

瀏覽 dist 資料夾：

```
npm run preview
```

如果未來要上線，要上線的會是 **`dist`** 資料夾。



