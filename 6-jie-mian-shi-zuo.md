# 6 實作

## 練習 1：checkbox 全選

給定以下 html：

{% code lineNumbers="true" %}
```html
<div id="check_block">
  <input type="checkbox" id="check_all" ref="my_check_all" @click="check_all_items"><label for="check_all">全選</label>

  <hr>

  <input type="checkbox" class="item" id="option1" @click="item_click"> <label for="option1">選項一</label>
  <input type="checkbox" class="item" id="option2" @click="item_click"> <label for="option2">選項二</label>
  <input type="checkbox" class="item" id="option3" @click="item_click"> <label for="option3">選項三</label>
</div>
```
{% endcode %}



{% embed url="https://codepen.io/carlos411/pen/rNvaVJK" %}





## 練習 2：分頁器



## 練習 3：頁籤

設定多個元件，然後做元件的顯示切換。

使用 **`<component :is=""></component>`** 標籤，動態的決定要顯示哪個元件。



如下示意圖：

![](.gitbook/assets/dynamic\_components.png)



範例網址：[https://codepen.io/carlos411/pen/eYegrWx](https://codepen.io/carlos411/pen/eYegrWx)

{% embed url="https://codepen.io/carlos411/pen/eYegrWx" %}



在 `practice` 資料夾下，建立 `ex3_tab.html` 檔案，將上方 CodePen 的範例，放到頁面當中，也要能夠正常運作。

