<template>
  <div id="app">
    <div>
      {{ msg }}
      <tinymce-editor ref="editor" v-model="msg" :disabled="disabled" @change="change"></tinymce-editor>
      <button @click="clear">清空内容</button>
      <button @click="disabled=true">禁用</button>
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
      { url: 'http://cued.xunlei.com/demos/publ/img/P_101.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_102.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_103.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_105.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_106.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_107.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_108.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_109.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_111.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_112.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_113.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_115.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_116.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_117.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_118.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_119.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_121.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_122.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_123.jpg' },
      { url: 'http://cued.xunlei.com/demos/publ/img/P_125.jpg' }
    ];
    waterfall(list, 'waterfall');
  },
  methods: {
    change(e, editor) {
      // console.log('Element clicked', e, editor);
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
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
}
</style>