<template>
  <div id="app">
    <div>
      <p style="white-space: pre;">{{ msg }}</p>
      <tinymce-editor ref="editor" v-model="msg" :disabled="disabled" @blur="handleBlur"></tinymce-editor>
      <button type="button" @click="clear" style="margin: 10px;">清空内容</button>
      <button type="button" @click="disabled=true">禁用</button>
    </div>
    <ul id="waterfall"></ul>
  </div>
</template>
<script>
import TinymceEditor from './components/Editor'
import { waterfall } from 'js-responsive-waterfall'

export default {
  name: 'app',
  components: {
    TinymceEditor
  },
  data() {
    return {
      msg: 'Welcome to Use Tinymce Editor',
      disabled: false
    }
  },
  mounted() {
    let list = [
      { url: 'https://p.upyun.com/demo/webp/webp/animated-gif-0.webp' },
      { url: 'https://p.upyun.com/demo/webp/webp/gif-0.webp' },
      { url: 'https://p.upyun.com/demo/webp/webp/png-0.webp' },
      { url: 'https://p.upyun.com/demo/webp/webp/jpg-0.webp' },
      { url: 'https://p.upyun.com/demo/webp/webp/gif-1.webp' },
      { url: 'https://p.upyun.com/demo/webp/webp/jpg-1.webp' }
    ];
    waterfall(list, 'waterfall');
  },
  mounted() {
    window.onbeforeunload = (e) => {
      e = e || window.event;
      // 兼容IE8和Firefox 4之前的版本
      if (e) e.returnValue = '确定要离开此页吗？';
      // Chrome, Safari, Firefox 4+, Opera 12+ , IE 9+
      return '确定要离开此页吗？';
    }
  },
  methods: {
    handleBlur(editor) {
      if (confirm('是否保存？')) alert('保存成功');
    },
    clear() {
      this.$refs.editor.clear();
    }
  }
}
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
}

button {
  cursor: pointer;
}
</style>