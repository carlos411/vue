# 7 認識 Vue Plugin 寫法

## 範例 1：簡易 Plugin

在 `practice` 資料夾下，建立 **`plugin1_simple.html`**，內容如下：

{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <h1>Custom Vue Plugin</h1>
    <div id="app">
    </div>

    <script src="./vendors/vue/vue.global.js"></script>
    <script>

      const myFirstPlugin = {
        install(app, options){
          console.log("Hello, Plugin!");
          console.log(options);
        }
      };

      Vue.createApp({}).use(myFirstPlugin, {option1: true}).mount("#app");
    </script>
  </body>
</html>
```
{% endcode %}



## 範例 2：Plugin 獨立至資料夾

在 `practice` 資料夾下，建立 **`plugin2_file.html`**，內容如下：

{% tabs %}
{% tab title="plugin2_file.html" %}
{% code lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <h1>Custom Vue Plugin 2</h1>
    <div id="app">
    </div>

    <script src="./vendors/vue/vue.global.js"></script>
    <script type="module" src="./js/plugin2_file.js"></script>
  </body>
</html>
```
{% endcode %}
{% endtab %}

{% tab title="js/plugin2_file.js" %}
{% code lineNumbers="true" %}
```javascript
import { myFirstPlugin } from "../plugins/myFirstPlugin/index.js";

Vue.createApp({}).use(myFirstPlugin, {option1: true}).mount("#app");
```
{% endcode %}
{% endtab %}
{% endtabs %}

然後在 `practice` 資料夾下，建立 **`plugins/myFirstPlugin/index.js`** 檔案，內容如下：

{% code lineNumbers="true" %}
```javascript
// 寫法一
export const myFirstPlugin = {
  install(app, options){
    console.log("Hello, Plugin!");
    console.log(options);
  }
};

// 寫法二
/*
export function myFirstPlugin(app, options){
  console.log("Hello, Plugin!");
  console.log(options);
}
*/
```
{% endcode %}



