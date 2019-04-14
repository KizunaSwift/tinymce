<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div>
      {{ msg }}
      <tinymce-editor
        ref="editor"
        v-model="msg" 
        :disabled="disabled" 
        @change="change" 
        ></tinymce-editor>
      <button @click="clear">清空内容</button>
      <button @click="disabled=true">禁用</button>
    </div>
  </div>
</template>
<script>
import HelloWorld from './components/HelloWorld'
import TinymceEditor from './components/editor'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TinymceEditor
  },
  data() {
    return {
      msg: 'Welcome to Use Tinymce Editor',
      disabled: false
    }
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
</style>