# 6 作業

## 前置

將原來 jQuery 的作業，複製一份，放到 **`assignment_vue`** 資料夾底下。然後執行以下幾點：

1. 在 assignment\_vue 資料夾下，建立 components 資料夾。
2. 將 js/index.js 檔案，所有原始碼刪除。
3. 在 vendors 資料夾底下，建立 vue 資料夾，裡面放入 **`vue.global.prod.js`** 檔案。
4. 更新 index.html 及 js/index.js 原始碼如下。

`index.html` 原始碼如下：

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>

    <link rel="stylesheet" href="./css/index.css">
  </head>
  <body>

    <article class="task_container" id="task_container">

      <button type="button" class="btn_empty">清空</button>

      <h1 class="title1">任務管理</h1>

      <div class="task_add_block">
        <input type="text" class="task_name" placeholder="輸入待辦事項…">
        <button type="button" class="task_add">新增</button>
      </div>

      <div class="task_list_parent">

        <ul class="task_list">
        </ul>

      </div>
    </article>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.13.0/js/all.min.js"></script>
    <script src="./vendors/vue/vue.global.prod.js"></script>
    <script src="./js/index.js" type="module"></script>
  </body>
</html>

```
{% endcode %}

`js/index.js` 的原始碼如下：

{% code lineNumbers="true" %}
```javascript
const app = Vue.createApp({});

app.mount("#task_container");
```
{% endcode %}



## 第 1 步：

完成以下項目：

* `input.task_name` 在 focus 事件觸發時，`div.task_add_block` 加上 `-on` class。
* `input.task_name` 在 blur 事件觸發時，`div.task_add_block` 移除 `-on` class。



## 3 使用 slot 標籤實作 fencyList

### 未使用 slot 標籤的版本

建立 `components/FencyList.js` 檔案，內容如下：

```javascript
export default {
  props: ["api-url"],
  data(){
    return {
      items: []
    };
  },
  template: `
    <ul>
      <li v-if="items.length == 0">Loading...</li>
      <li v-for="(my_item, i) in items">
        項目 id: {{ my_item.id }},
        標題: {{ my_item.title }},
        使用者 id: {{ my_item.userId }}
      </li>
    </ul>
  `,
  mounted(){
    //console.log(this.apiUrl);
    fetch(this.apiUrl).then((res) => res.json()).then((body) => {
      //console.log(body);
      this.items = body
    });
  }
}
```



在 `practice` 資料夾下，建立 `component8_list.html` 檔案，內容如下：

```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div id="myapp">

      <fency-list api-url="https://jsonplaceholder.typicode.com/todos"></fency-list>

    </div>

    <script src="./vendors/vue/vue.global.js"></script>

    <script type="module">
      import FencyList from "./components/FencyList.js";

      const app = Vue.createApp({});

      app.component("FencyList", FencyList);
      app.mount("#myapp");
    </script>
  </body>
</html>
```



### 完成版：使用 slot

最後 `components/FencyList.js` 檔案，完成的內容如下：

```javascript
export default {
  props: ["api-url"],
  data(){
    return {
      items: []
    };
  },
  template: `
    <ul>
      <li v-if="items.length == 0">Loading...</li>
      <li v-for="(my_item, i) in items">
        <slot name="content" :data="my_item"></slot>
      </li>
    </ul>
  `,
  mounted(){
    //console.log(this.apiUrl);
    fetch(this.apiUrl).then((res) => res.json()).then((body) => {
      //console.log(body);
      this.items = body
    });
  }
}
```



最後 `component8_list.html` 檔案，完成的內容如下：

```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div id="myapp">

      <fency-list api-url="https://jsonplaceholder.typicode.com/todos">

        <template v-slot:content="item">
          <div class="item_block" style="border: 1px solid red;">
            項目 id: {{ item.data.id }},
            標題: {{ item.data.title }},
            使用者 id: {{ item.data.userId }}
          </div>
        </template>

      </fency-list>

    </div>

    <script src="./vendors/vue/vue.global.js"></script>

    <script type="module">
      import FencyList from "./components/FencyList.js";

      const app = Vue.createApp({});

      app.component("FencyList", FencyList);
      app.mount("#myapp");
    </script>
  </body>
</html>

```





