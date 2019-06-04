<template>
  <div id="app">
    <img src="./assets/logo.png">
    <!-- 插值之文本，数据绑定最常见的形式就是使用 {{...}}（双大括号）的文本插值 -->
    <h1>{{ msg }}</h1>
    <h1>My English Name is {{ name }}</h1>
    <firstComponent></firstComponent>
    <ul>
      <li><router-link to="/first">第一页</router-link></li>
      <li><router-link to="/second">第二页</router-link></li>
    </ul>
    <router-view class="view"></router-view>
    <a href="vue2-learn/src/test.html" target="_blank">测试用例</a>
    <p>实现视图层的新增、删除、修改、查看功能</p>
    <h1>site : {{site}}</h1>
    <h1>url : {{url}}</h1>
    <h1>{{details()}}</h1>
    <!-- 插值之Html，使用 v-html 指令用于输出 html 代码-->
    <h1 v-html="msg"></h1>
    <!-- 插值之属性，HTML 属性中的值应使用 v-bind 指令。以下实例判断 class1 的值，
    如果为 true 使用 class1 类的样式，否则不使用该类：-->
    <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
    <br><br>
    <div v-bind:class="{'class1': use}">
      v-bind:class 指令
    </div>
    <!-- 插值之表达式，Vue.js 都提供了完全的 JavaScript 表达式支持。 -->
    {{5 + 5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ ok2 ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list_' + id">杰克思勒的博客</div>
    <!-- 插值之指令，指令是带有 v- 前缀的特殊属性。指令用于在表达式的值改变时，将某些行为应用到 DOM 上，
    这里， v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。-->
    <p v-if="seen">现在你看到我了</p>
    <!-- 插值之参数，参数在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：
    在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。-->
    <pre><a v-bind:href="url" target="_blank">{{site}}</a></pre>
    <!-- 插值修饰符，修饰符是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。
    例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()： -->
    <form v-on:submit.prevent="onSubmit">
      <input type="text" name="userName" placeholder="用户名" />
      <input type="text" name="password" placeholder="密码" />
      <button type="submit">登录</button>
    </form>
    <h1>修改功能</h1>
    <!--  v-on 指令，它用于监听 DOM 事件，在这里参数是监听的事件名。 -->
    <button v-on:click="changeSite">修改功能之修改site</button>
  </div>
</template>
<script src="js/vue.min.js"></script>
<script>
  import firstComponent from './component/firstComponent.vue';
  export default {
    data() {
      return {
        msg: 'Hello Vue!',
        name: 'Jef',
        site: "杰克思勒的博客",
        url: "https://www.cnblogs.com/tufujie/",
        use: false,
        ok: true,
        ok2: false,
        message: 'JavaScript 表达式支持',
        id : 1,
        seen: true,
        userName: ""
      }
    },
    methods: {
      details: function() {
        // 返回值
        return  this.site + " - 学习技术！";
      },
      changeSite() {
        // 触发事件
        this.site = "JackSile's Blog";
      },
      onSubmit() {
        this.userName = $.trim($('input[name="userName"]').val());
        // 提交触发事件
        if (this.userName == 'Jef') {
            alert('登录成功');
        } else {
          alert('登录失败');
        }
      }
    },
    components: { firstComponent }
  };
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.class1 {
  background: #444;
  color: #eee;
}
</style>
