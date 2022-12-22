# 6 介面實作

## 練習 1：checkbox 全選

在 `practice` 資料夾下，建立 `ex1_checkbox.html` 檔案。

第一步，貼以下的原始碼，將 items 陣列在畫面上渲染出來(底下 template 標籤的部份)：

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div id="app">
      <input type="checkbox" id="check_all"><label for="check_all">全選</label>
    
      <hr>
      <template v-for="item in items" :key="item.id">
        <input type="checkbox" id="" value="">
        <label for="">選項{{item.value}}</label>
      </template>
    </div>

    <script src="./vendors/vue/vue.global.js"></script>
    <!-- <script src="./vendors/vue/vue.global.prod.js"></script> -->

    <script>
      const RootComponent = {
        data(){
          return {
            items: [
              {
                id: "option1",
                value: "a"
              },
              {
                id: "option2",
                value: "b"
              },
              {
                id: "option3",
                value: "c"
              }
            ]
          };
        },
        computed: {
          
        },
        methods: {
          
        }
      };
      Vue.createApp(RootComponent).mount("#app");
    </script>
  </body>
</html>
```
{% endcode %}



第二步：

在 data 函式回傳的資料當中，加一個 checkedItems 空陣列，且要跟選項的 checkbox 做綁定(使用 `v-model`)。

然後請使用 vue 的 devtools 來觀察。



第三步：

在 computed 物件中，加：

{% code lineNumbers="true" %}
```javascript
isCheckAll(e){
  return this.checkedItems.length == this.items.length;
}
```
{% endcode %}

然後全選的 checkbox，加以下的屬性綁定：

{% code lineNumbers="true" %}
```javascript
:checked="isCheckAll"
```
{% endcode %}



第四步：

替全選的 checkbox，做 click 事件上的綁定：

{% code lineNumbers="true" %}
```javascript
@click="checkAllItems"
```
{% endcode %}

然後在 methods 物件中，加：

{% code lineNumbers="true" %}
```javascript
checkAllItems(e){
  //console.log(this.isCheckAll);
  if(this.isCheckAll){
    this.checkedItems = [];
  }else{
    let arr = [];
    this.items.forEach((item, i) => {
      arr.push(item.value);
    });
    this.checkedItems = arr;
  }
}
```
{% endcode %}



參考作法：

{% embed url="https://codepen.io/carlos411/pen/eYjOGzE" %}



## 練習 2：分頁器

在 `practice` 資料夾下，建立 `ex2_paginator.html` 檔案，內容如下：

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
    <style>
      div.pagination_block{
        display: inline-block;
      }
      div.pagination_block > ul.pagination{
        list-style: none;
        margin: 0;
        padding: 0;
        font-size: 0;
      }
      div.pagination_block > ul.pagination > li{
        display: inline-block;
      }
      div.pagination_block > ul.pagination > li > a{
        display: inline-block;
        text-decoration: none;

        border: 1px solid #dee2e6; /* 留意 */
        border-right: 0;           /* 留意：將全部的右邊框都移除 */

        text-align: center;
        padding: 5px 10px;
        font-size: 1rem;
        color: #007bff;
      }

      /* 留意: 將最後一個 li 裡的 a，右邊框加回來 */
      /* 留意: 將最後一個 li 裡的 a，加上圓角 */
      div.pagination_block > ul.pagination > li:last-child > a{
        border-right: 1px solid #dee2e6;
        border-radius: 0 5px 5px 0;
      }
      /* 留意: 將第一個 li 裡的 a，加上圓角 */
      div.pagination_block > ul.pagination > li:first-child > a{
        display: inline-block;
        border-radius: 5px 0 0 5px;
      }

      div.pagination_block > ul.pagination > li > a.-on{
        background-color: #e9ecef;
        color: #0056b3;
      }

      div.pagination_block > ul.pagination > li > a:hover{
        background-color: #e9ecef;
        color: #0056b3;
      }
    </style>
  </head>
  <body>
    <div class="pagination_block" id="pagination_block">
      <ul class="pagination">
        <li><a href="#">&lt;</a></li>
        <li><a href="#" class="-on">1</a></li>
        <li><a href="#" >2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">6</a></li>
        <li><a href="#">7</a></li>
        <li><a href="#">8</a></li>
        <li><a href="#">9</a></li>
        <li><a href="#">10</a></li>
        <li><a href="#">&gt;</a></li>
      </ul>
    </div>
    
    <script src="./vendors/vue/vue.global.js"></script>
    <!-- <script src="./vendors/vue/vue.global.prod.js"></script> -->
  </body>
</html>
```
{% endcode %}



第一步：

請建立 **`the-paginator`** 標籤(即 **`ThePaginator 元件`**)，產出的畫面結果要與上述程式碼相同，如下(僅列出 body 標籤的部份)：

{% code lineNumbers="true" %}
```html
<div id="paginator_block">
  <the-paginator></the-paginator>
</div>

<script src="./vendors/vue/vue.global.js"></script>
<!-- <script src="./vendors/vue/vue.global.prod.js"></script> -->

<script type="module">
  import ThePaginator from "./components/ThePaginator.js";

  Vue.createApp({}).component("ThePaginator", ThePaginator).mount("#paginator_block");
</script>
```
{% endcode %}

請練習撰寫 **`./components/ThePaginator.js`** 。寫完的結果如下 codepen：

{% embed url="https://codepen.io/carlos411/pen/LYmBoYj" %}



第二步：

讓 ThePaginator 元件，可帶入三個參數：

* `total-items`：總共有幾筆資料。
* `items-per-page`：每頁顯示幾筆資料。
* `current-page`：目前在第幾頁。



故可使用 ThePaginator 元件，如下原始碼：

{% code lineNumbers="true" %}
```html
<the-paginator total-items="99" items-per-page="10" current-page="2"></the-paginator>
```
{% endcode %}

那 **`./components/ThePaginator.js`**  應如何改寫？

* 加 props 屬性，是一個陣列，放入三個資料(`totalItems`、`itemsPerPage`、`currentPage`)。
* 加一個 totalPages 的計算屬性(computed properties)，計算出總頁數。
* template 屬性，修改樣版。

寫完後，如下 codepen：

{% embed url="https://codepen.io/carlos411/pen/OJZwYXd" %}



## 練習 3：頁籤

設定多個元件，然後做元件的顯示切換。

可使用 **`<component :is="元件名稱"></component>`** 標籤，動態的決定要顯示哪個元件名稱。



第一步，在 `practice` 資料夾下，建立 `ex3_tab.html` 檔案，貼以下的原始嗎

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
    <style>
      .active{
        background-color: red;
        color: white;
      }
      .tab_content{
        border: 1px solid lightgray;
        padding: 10px;
        margin-top: 5px;
      }
    </style>
  </head>
  <body>
    <div id="the_block">
      <button type="button">{{ tab.name }}</button>

    </div>
    
    <script src="./vendors/vue/vue.global.js"></script>
    <!-- <script src="./vendors/vue/vue.global.prod.js"></script> -->
    
    <script type="module">
      var app = Vue.createApp({
        data(){
          return {
            currentTab: "tab1",
            tabs: [
              {
                id: "tab1",
                name: "頁籤一"
              },
              {
                id: "tab2",
                name: "頁籤二"
              },
              {
                id: "tab3",
                name: "頁籤三"
              }
            ]
          };
        }
      });

      app.mount("#the_block");
    </script>
  </body>
</html>
```
{% endcode %}

* button 標籤依據 tabs 資料，跑迴圈，跑出三個按鈕。
* 如果資料 currentTab 是 tab1 或 tab2 或 tab3，那所對應的按鈕，就加 active 這個 class。
* 按鈕點擊的時候，無將 id 的值，設定到 currentTab。
* 標籤裡的文字，就是 name 的部份。
* key 的部份，也要設定，`:key="tab.id"`。

改完後，按鈕如下原始碼：

{% code lineNumbers="true" %}
```html
<button type="button" v-for="tab in tabs" :class="{active: currentTab == tab.id}" :key="tab.id" @click="currentTab = tab.id">{{ tab.name }}</button>
```
{% endcode %}



第二步，以全域方式，載入三個元件，原始碼如下，請貼到恰當位置：

{% code lineNumbers="true" %}
```javascript
app.component("tab1_content", {
  template: `
    <div class="a">tab1 的內容</div>
  `
});

app.component("tab2_content", {
  template: `
    <div class="b">tab2 的內容</div>
  `
});

app.component("tab3_content", {
  template: `
    <div class="c">tab3 的內容</div>
  `
});
```
{% endcode %}



第三步，設定一個計算屬性叫做 current\_tab\_component，回傳的會是元件名稱，元素始如下，請放到恰當位置：

{% code lineNumbers="true" %}
```javascript
computed: {
  current_tab_component(){
    return this.currentTab + "_content";
  }
}
```
{% endcode %}



第四步，使用 component 標籤，來決定要顯示哪一個元件：

{% code lineNumbers="true" %}
```html
<component v-bind:is="current_tab_component" class="tab_content"></component>
```
{% endcode %}



如下示意圖：

![](.gitbook/assets/dynamic\_components.png)



範例網址：[https://codepen.io/carlos411/pen/eYegrWx](https://codepen.io/carlos411/pen/eYegrWx)

{% embed url="https://codepen.io/carlos411/pen/eYegrWx" %}





