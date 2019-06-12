<template>
  <div id="app">
    <img src="./assets/logo.png">
    <!-- 插值之文本，数据绑定最常见的形式就是使用 {{...}}（双大括号）的文本插值 -->
    <h1>{{ msg }}</h1>
    <h1>My English Name is {{ name }}</h1>
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
    <!-- 插值之表达式，Vue.js 都提供了完全的 JavaScript 表达式支持。 -->
    {{5 + 5}}<br/>
    {{ ok ? 'YES' : 'NO' }}<br/>
    {{ ok2 ? 'YES' : 'NO' }}<br/>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list_' + id">杰克思勒的博客</div>
    <!-- 插值之参数，参数在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：
    在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。-->
    <pre><a v-bind:href="url" target="_blank">{{site}}</a></pre>
    <h1>Vue.js 表单</h1>
    <!-- 插值修饰符，修饰符是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。
    例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()： -->
    <form v-on:submit.prevent="onSubmit">
      <input type="text" name="userName" placeholder="用户名" v-model="userName" />
      <input type="text" name="password" placeholder="密码" v-model="password" />
      <button type="submit">登录</button>
    </form>
    <!-- 多行文本输入 -->
    <textarea v-model="message2" placeholder="多行文本输入……"></textarea>
   <!-- 用户输入，在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定，
   修改了v-model="userName"的值后，this.userName会进行修改，从而实现了双向绑定-->
    <!-- v-model 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，
    根据表单上的值，自动更新绑定的元素的值。按钮的事件我们可以使用 v-on 监听事件，并对用户的输入进行响应。
    以下实例在用户点击按钮后对字符串进行反转操作：-->
    <!-- 复选框，复选框如果是一个为逻辑值，如果是多个则绑定到同一个数组： -->
    <p>单个复选框：</p>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>

    <p>多个复选框：</p>
    <input type="checkbox" id="baidu" value="Baidu" v-model="checkedNames">
    <label for="baidu">Baidu</label>
    <input type="checkbox" id="google" value="Google" v-model="checkedNames">
    <label for="google">Google</label>
    <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames">
    <label for="taobao">Taobao</label>
    <br/>
    <span>选择的值为: {{ checkedNames }}</span><br/>
    <input type="radio" id="tencent" value="Tencent" v-model="picked">
    <label for="tencent">Tencent</label>
    <br/>
    <input type="radio" id="alibaba" value="Alibaba" v-model="picked">
    <label for="alibaba">Alibaba</label>
    <br/>
    <span>选中值为: {{ picked }}</span>
    <br/>
    <select v-model="selected" name="fruit">
      <option value="">选择一个网站</option>
      <option value="www.baidu.com">Baidu</option>
      <option value="www.google.com">Google</option>
    </select>
    <div id="output">
      选择的网站是: {{selected}}
    </div>
   <!-- 修饰符
    .lazy
    在默认情况下， v-model 在 input 事件中同步输入框的值与数据，但你可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步：-->
    <!-- 在 "change" 而不是 "input" 事件中更新 -->
    <input v-model.lazy="userName" />
   <!-- .number
    如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值：-->
    <input v-model.number="age" type="number" />
    <!--这通常很有用，因为在 type="number" 时 HTML 中输入的值也总是会返回字符串类型。
    .trim
    如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入：-->
    <input v-model.trim="userName" />
    <h1>修改功能</h1>
    <!--  v-on 指令，它用于监听 DOM 事件，在这里参数是监听的事件名。 -->
    <!-- v-on 可以接收一个定义的方法来调用。 -->
    <button v-on:click="changeSite">修改功能之修改site</button>
    <button v-on:click="say('Hi')">用内联 JavaScript 语句</button>
    <input v-on:keyup.enter="submit" @keyup.alt.67="clear" v-model="userName" />
    <!-- 过滤器，Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下： -->
    <!-- 在两个大括号中 -->
    <p>{{ message | capitalize }}</p>
    <!-- 在 v-bind 指令中 -->
    <div v-bind:id="rawId | formatId">
      <p>filters</p>
    </div>
    <!-- 过滤器函数接受表达式的值作为第一个参数。-->
    <!--
    过滤器可以串联：
    {{ message | filterA | filterB }}
    过滤器是 JavaScript 函数，因此可以接受参数：
    {{ message | filterA('arg1', arg2) }}
    这里，message 是第一个参数，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。
    -->
    <!-- 缩写 -->
    <!-- Vue.js 为两个最为常用的指令提供了特别的缩写： -->
    <!-- v-bind 缩写 -->
    <!-- 完整语法 -->
    <a v-bind:href="url" target="_blank">{{site}}</a>
    <!-- 缩写 -->
    <a :href="url" target="_blank">{{site}}</a>
    <!-- v-on 缩写 -->
    <!-- 完整语法 -->
    <button v-on:click="doSomething">doSomeThing</button>
    <!-- 缩写 -->
    <button @click="doSomething">doSomething</button>
    <!-- Vue.js 条件语句 -->
    <!-- 条件判断 -->
    <!-- 插值之指令，指令是带有 v- 前缀的特殊属性。指令用于在表达式的值改变时，将某些行为应用到 DOM 上，
    这里， v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。-->
    <p v-if="seen">现在你看到我了</p>
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
    <!-- v-show，我们也可以使用 v-show 指令来根据条件展示元素：-->
    <h1 v-show="ok">{{msg}}</h1>
    <!-- 循环语句 -->
    <!-- 循环使用 v-for 指令。
    v-for 指令需要以 site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。
    v-for 可以绑定数据到数组来渲染一个列表： -->
    <ol>
      <li v-for="site in sites">{{site.name}}</li>
    </ol>
    <ul>
      <li v-for="value in info">
        {{ value }}
      </li>
    </ul>
    <!-- 第二个的参数为键名：第三个参数为索引： -->
    <ul>
      <li v-for="(value, key, index) in info">
        {{index}} -> {{key}} : {{ value }}
      </li>
    </ul>
    <!-- v-for 迭代整数，v-for 也可以循环整数 -->
    <ul>
      <li v-for="i in 10">
        {{i}}
      </li>
    </ul>
    <!-- Vue.js 计算属性 -->
    <!-- 计算属性关键词: computed。计算属性在处理一些复杂逻辑时是很有用的。 -->
    <p>原始字符串: {{ message }}</p>
    <p>计算后反转字符串: {{ reversedMessage }}</p>
    <p>computedFromOne: {{ computedFromOne }}</p>
    <p>computedFromTwo: {{ computedFromTwo }}</p>
    <p>computedResult: {{ computedResult }}</p>
    <p v-on:click="changeComputed">computedResult修改</p>
    <!-- Vue.js 监听属性 -->
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button><br/>
    千米 : <input type = "text" v-model = "kilometers">
    米 : <input type = "text" v-model = "meters"><br/>
    <!-- Vue.js 样式绑定 -->
    <!-- 插值之属性，HTML 属性中的值应使用 v-bind 指令。以下实例判断 class1 的值，
    如果为 true 使用 class1 类的样式，否则不使用该类：-->
    <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
    <br/><br/>
    <div v-bind:class="{'class1': use}">
      v-bind:class 指令
    </div>
    <div v-bind:class="classObject"></div><br/>
    <!-- 数组语法 -->
    <div v-bind:class="[base, activeClass, errorClass]"></div><br/>
    <div v-bind:class="[base, errorClass, isActive ? activeClass : '']"></div>
    <div v-bind:style="styleObject">{{name}}</div>
    <div v-bind:style="[baseStyles, overridingStyles]">{{name}}</div>
    <!-- Vue.js 事件处理器 -->
    <h1>Vue.js 组件</h1>
    <div>
      <input v-model="parentMsg">
      <br>
      <child v-bind:message="parentMsg"></child>
    </div>
    <ol>
      <site-item v-for="item in sites" v-bind:siteItem="item"></site-item>
    </ol>
    <validateComponent v-bind:validateNum="123"></validateComponent>



    <br/>
    <helloCompnent message="Hello Vue!"></helloCompnent>
    <authorComponent></authorComponent>
  </div>
</template>
<script src="js/vue.min.js"></script>
<script>
  import Vue from 'vue';
  // 定义组件, 也可以从别的文件引入
  let authorComponent = {template: ' <a> author by Jef </a>' };
  let name = "Jef", url = "https://www.cnblogs.com/tufujie/", goal = "感受代码魅力，享受美好人生！";
  export default {
    data() {
      return {
        // 放置初始化的值
        msg: 'Hello Vue!',
        name: name,
        site: "杰克思勒的博客",
        url: url,
        use: false,
        ok: true,
        ok2: false,
        message: 'JavaScript 表达式支持',
        id : 1,
        seen: true,
        userName: "",
        password: "",
        message: "hello vue!",
        rawId: "1234567890123456789012345678901234567890",
        type: "B",
        goal: goal,
        sites: [
          { name: 'Baidu' },
          { name: 'Google' },
          { name: 'Taobao' }
        ],
        info: {
          name: name,
          url: url,
          goal: goal
        },
        computedFromOne: "One",
        computedFromTwo: "two",
        counter: 1,
        kilometers: 0,
        meters: 0,
        hasError: false,
        isActive: true,
        resultData: {
          result: "success",
          data: null,
          msg: "操作成功",
          code: 0,
          success: true
        },
        activeClass: 'active',
        errorClass: 'text-danger',
        base: "base",
        styleObject: {
          color: 'green',
          fontSize: '30px'
        },
        baseStyles: {
          color: 'green',
          fontSize: '30px'
        },
        overridingStyles: {
          'font-weight': 'bold'
        },
        message2: "多行文本",
        checked : false,
        checkedNames: [],
        picked: "Tecent",
        selected: '',
        age: 18,
        parentMsg: '父组件内容'
      }
    },
    methods: {
      details: function() {
        // 返回值
        return this.site + " - 学习技术！";
      },
      changeSite(event) {
        // 触发事件
        this.site = "JackSile's Blog";
        if (event) {
          alert(event.target.tagName)
        }
      },
      onSubmit() {
        // this.userName = $.trim($('input[name="userName"]').val());
        // 提交触发事件
        if (this.userName == 'Jef') {
            alert(this.userName + '登录成功');
        } else {
          alert(this.userName + '登录失败');
        }
      },
      doSomething() {
        alert("doSomeThing");
      },
      changeComputed() {
        // 调用setter
        this.computedResult = 'fromOneChange fromTwoChange';
      },
      say: function(sayWord) {
        alert(this.name + "," + sayWord);
      },
      submit: function () {
        alert("submit");
      },
      clear: function () {
        this.userName = '';
      }
    },
    filters: {
      capitalize: function (value) {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1);
      },
      // 保留32位字符
      formatId: function (value) {
        if (!value) return '';
        value = value.toString();
        return value.substring(0, 32);
      }
    },
    computed: {
      // 计算属性的 getter
      reversedMessage: function () {
        // `this` 指向 vm 实例
        // reversedMessage 依赖于 vm.message，在 vm.message 发生改变时，vm.reversedMessage 也会更新
        // computed vs methods
        // 我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。
        // 而使用 methods ，在重新渲染的时候，函数总会重新调用执行。
        // 可以说使用 computed 性能会更好，但是如果你不希望缓存，你可以使用 methods 属性。
        // computed setter
        // computed 属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：
        return this.message.split('').reverse().join('');
      },
      computedResult: {
        // getter
        get: function () {
          return this.computedFromOne + ' ' + this.computedFromTwo;
        },
        // setter
        set: function (newValue) {
          var computedResult = newValue.split(' ')
          this.computedFromOne = computedResult[0]
          this.computedFromTwo = computedResult[computedResult.length - 1]
        }
      },
      classObject: function () {
        // 添加class样式
        let activeAdd = false, dangerAdd = false;
        if (this.resultData.success) {
          activeAdd = true;
        } else {
          dangerAdd = true;
        }
        return {
          base: true,
          active: activeAdd,
          'text-danger': dangerAdd
        }
      }
    },
    watch: {
      kilometers: function(val) {
        this.kilometers = val;
        this.meters = this.kilometers * 1000
      },
      meters: function (val) {
        this.kilometers = val / 1000;
        this.meters = val;
      }
    },
    //  组件形式为：'authorComponent': authorComponent，如果不修改名称的前提下可以直接用authorComponent
    components: { authorComponent },
  };
  // 注册
  Vue.component('helloCompnent', {
    // 声明 props
    props: ['message'],
    // 同样也可以在 vm 实例中像 “this.message” 这样使用
    template: '<span>{{ message }}</span>'
  });
  Vue.component('child', {
    // 声明 props
    props: ['message'],
    // 同样也可以在 vm 实例中像 “this.message” 这样使用
    template: '<span>{{ message }}</span>'
  });
  Vue.component('site-item', {
    props: ['siteItem'],
    template: '<li>{{ siteItem.name }}</li>'
  });
  Vue.component('validateComponent', {
    props: {
      validateNum: {
        type: Number,
        default: 100
      }
    },
    template: '<input type="text" name="validateText" v-bind:validateNum="123">'
  });
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

.base {
  width: 100px;
  height: 100px;
}

.active {
  background: green;
}

.text-danger {
  background: red;
}
</style>
