# 6 介面實作

## 練習 1：checkbox 全選

在 `practice` 資料夾下，建立 `ex1_checkbox.html` 檔案，直接貼以下的原始碼來解讀：

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
      <input type="checkbox" id="check_all" :checked="isCheckAll" @click="checkAllItems"><label for="check_all">全選</label>
    
      <hr>
      
      <template v-for="item in items" :key="item.id">
        <input type="checkbox" :id="item.id" :value="item.value" v-model="checkedItems">
        <label :for="item.id">選項{{item.value}}</label>
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
            ],
            checkedItems: []
          };
        },
        computed: {
          isCheckAll(e){
            return this.checkedItems.length == this.items.length;
          }
        },
        methods: {
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
        }
      };
      Vue.createApp(RootComponent).mount("#app");
    </script>
  </body>
</html>
```
{% endcode %}



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

請建立 **`the-paginator`** 標籤(即 ThePaginator 元件)，產出的畫面結果要與上述程式碼相同，如下(僅列出 body 標籤的部份)：

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

請練習撰寫 **`./components/ThePaginator.js`** 。



參考作法如下 codepen：

{% embed url="https://codepen.io/carlos411/pen/LYmBoYj" %}



該 ThePaginator 元件，可帶入三個參數：

* `total-items`：總共有幾筆資料。
* `items-per-page`：每頁顯示幾筆資料。
* `current-page`：目前在第幾頁。



故使用 ThePaginator 元件，如下原始碼：

{% code lineNumbers="true" %}
```html
<the-paginator total-items="99" items-per-page="10" current-page="2"></the-paginator>
```
{% endcode %}

那 **`./components/ThePaginator.js`**  應如何改寫？



參考作法：

{% embed url="https://codepen.io/carlos411/pen/OJZwYXd" %}



## 練習 3：頁籤

設定多個元件，然後做元件的顯示切換。

使用 **`<component :is=""></component>`** 標籤，動態的決定要顯示哪個元件。



如下示意圖：

![](.gitbook/assets/dynamic\_components.png)



範例網址：[https://codepen.io/carlos411/pen/eYegrWx](https://codepen.io/carlos411/pen/eYegrWx)

{% embed url="https://codepen.io/carlos411/pen/eYegrWx" %}



在 `practice` 資料夾下，建立 `ex3_tab.html` 檔案，將上方 CodePen 的範例，放到頁面當中，也要能夠正常運作。

