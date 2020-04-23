## 1. 在Vue项目中引入axios时的一些注意问题
- 使用 npm install 安装 axios
- 在main.js中
  - 引入 axios
  - 设置 Vue.prototype.axios = axios
- 以后在组件中可以这样使用: this.$axios
- 不要用vue add 来安装 axios

## 2. 使用axios从服务器取得数据后，
- 要注意数据的格式
- 最好在console验证数据格式是否符合要求

## 3. 代码例子：

```
import Vue from 'vue'
// import './plugins/axios'
import App from './App.vue'
import ElementUI from 'element-ui'
import axios from 'axios'
import 'element-ui/lib/theme-chalk/index.css'


Vue.use(ElementUI)
Vue.use(axios)
Vue.prototype.$axios = axios

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

## 4. 使用axios的例子

```
export default {
  name: "HelloWorld",
  data() {
    return {
      tableData: []
    };
  },
  mounted() {
    this.$axios({
      method: "get",
      headers: {
        "Content-Type": "application/json;charset=UTF-8"
      },
      url:
        "https://www.fastmock.site/mock/4a9df185ef4a62f4b6426b3339a8e227/api/api/users" // 接口地址
      // data: {
      //   keyword: "1" // 传接口参数
      // }
    })
      .then(response => {
        this.tableData = response.data.data;
        console.log(response.data.data, "success"); // 成功的返回
      })
      .catch(error => console.log(error, "error")); // 失败的返回
  }
}
```