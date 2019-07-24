<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <qriously :value="value" :size="size" :element="element" :background-alpha="backgroundAlpha" />
    <el-button type="success" plain @click="handleCopy(inputData,$event)">copy1</el-button>
    <el-button v-clipboard:copy="inputData" v-clipboard:success="clipboardSuccess" type="success" plain>copy2</el-button>
    <br><br>
    <div>{{ token }}</div>
    <el-button type="primary" plain @click="setlanguage('zh')">zh</el-button>
    <el-button type="primary" plain @click="setlanguage('en')">en</el-button>
    <el-button type="primary" plain @click="add()">addCookie</el-button>
    <el-button type="primary" plain @click="get()">getCookie</el-button>
    <el-button type="primary" plain @click="del()">delCookie</el-button>
    <el-button type="primary" plain @click="live()">to live</el-button>
    <el-button type="primary" plain @click="playback()">to playback</el-button>
    <el-button type="primary" plain @click="vueCropper()">to vueCropper</el-button>
    <br><br>
    <!--引入组件-->
    <tinymce :id="content" v-model="content" class="tinymce" :height="300" :width="900" :value="content" :toolbar="toolbar" :plugins="plugins" />
    <!--显示输入的文字-->
    <div class="editor-content" v-html="content" />
  </div>
</template>

<script>
// 直接使用
import clip from '@/utils/clipboard'
// 指令形式使用
import clipboard from '@/directive/clipboard/index.js'
import Tinymce from '@/components/Tinymce'
export default {
  name: 'HelloWorld',
  components: { Tinymce },
  directives: {
    clipboard
  },
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      token: null,
      // 可以自定义，必填项。
      value: 'http://lxchuan12.github.io/',
      // 二维码大小 默认 100
      size: 80,
      element: 'img',
      // 背景透明度，默认透明 0
      backgroundAlpha: 1,
      inputData: 'copy123456',
      content: 'Tinymce',
      toolbar: ['searchreplace bold italic underline strikethrough alignleft aligncenter alignright outdent indent  blockquote undo redo removeformat subscript superscript code codesample', 'hr bullist numlist link charmap preview anchor pagebreak insertdatetime table emoticons forecolor backcolor fullscreen'],
      plugins: ['advlist anchor autolink autosave code codesample colorpicker colorpicker contextmenu directionality emoticons fullscreen hr imagetools insertdatetime link lists nonbreaking noneditable pagebreak paste preview print save searchreplace spellchecker tabfocus table template textcolor textpattern visualblocks visualchars wordcount']
    }
  },
  methods: {
    handleCopy(text, event) {
      clip(text, event)
    },
    clipboardSuccess() {
      this.$message({
        message: '复制成功2',
        type: 'success',
        duration: 1500
      })
    },
    add() {
      this.token = this.$Cookies.set('token', '1111', { expires: 1 })
      const a = 1
      console.log(a)
    },
    del() {
      this.token = this.$Cookies.remove('token')
    },
    get() {
      this.token = this.$Cookies.get('token')
    },
    setlanguage(lang) {
      this.language = this.$Cookies.set('language', lang)
    },
    live() {
      this.$router.push({ path: '/live' })
    },
    playback() {
      this.$router.push({ path: '/playback' })
    },
    vueCropper() {
      this.$router.push({ path: '/examples/vueCropper' })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  .tinymce {
    margin-left: 100px;
  }
  .hello {
    text-align: center;
  }
</style>
