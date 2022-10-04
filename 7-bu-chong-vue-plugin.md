# 7 補充：Vue Plugin

## 範例 1：簡易 Plugin

在 practice 資料夾下，建立 **`plugin1_simple.html`**，內容如下：

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



