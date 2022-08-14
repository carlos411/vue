# 6 作業

文章分類頁

文章詳細頁



## 1 Checkbox 全選





## 2 breadcrumb 介面



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





