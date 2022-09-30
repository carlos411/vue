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

const vm = app.mount("#task_container");
```
{% endcode %}



## 第 1 步：text 欄位事件

完成以下項目：

* `input.task_name` 在 focus 事件觸發時，`div.task_add_block` 加上 `-on` class。
* `input.task_name` 在 blur 事件觸發時，`div.task_add_block` 移除 `-on` class。



## 第 2 步：新增

待辦事項一大串的 li：

{% code lineNumbers="true" %}
```html
<li>
  <div class="item_flex">
    <div class="left_block">
      <div class="btn_flex">
        <button type="button" class="btn_up">往上</button>
        <button type="button" class="btn_down">往下</button>
      </div>
    </div>
    <div class="middle_block">
      <div class="star_block">
        <span class="star" data-star="1"><i class="fas fa-star"></i></span>
        <span class="star" data-star="2"><i class="fas fa-star"></i></span>
        <span class="star" data-star="3"><i class="fas fa-star"></i></span>
        <span class="star" data-star="4"><i class="fas fa-star"></i></span>
        <span class="star" data-star="5"><i class="fas fa-star"></i></span>
      </div>
      <p class="para">這是任務這是任務這是任務這是任務這是任務這是任務這是任務這是任務這是任務這是任務這是任務這是任務</p>
      <input type="text" class="task_name_update -none" placeholder="更新待辦事項…">
    </div>
    <div class="right_block">
      <div class="btn_flex">
        <button type="button" class="btn_update">更新</button>
        <button type="button" class="btn_delete">移除</button>
      </div>
    </div>
  </div>
</li>
```
{% endcode %}



完成以下項目：

* 按下「新增」按鈕時，將待辦事項 html(一大串的 li)，新增到 `ul.task_list` 裡，新增到裡面的最前面。
* 如果沒有輸入待辦事項，按「新增」的話，不能有任何反應。
* 新增成功的話，待辦事項欄位要清空。
* 輸入的待辦事項，如果文字的最左邊、最右邊有空格，需移除。(語法：JS 內建的 `trim()` 函式)。
* 按下「Enter」鍵，也要能新增待辦事項。



## 第 3 步：移除與清空

完成以下項目：

* 按下「移除」按鈕，淡出 1 秒，然後移除該筆待辦事項。
* 按下「清空」按鈕，淡出 1 秒，清除全部的待辦事項。







