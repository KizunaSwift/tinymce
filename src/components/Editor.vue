<template>
  <div class="tinymce-editor">
    <editor ref="editor" v-model="myValue" :init="init" :disabled="disabled" @onClick="change" @onBlur="blur"></editor>
  </div>
</template>
<script>
import tinymce from 'tinymce/tinymce'
import Editor from '@tinymce/tinymce-vue'
import 'tinymce/themes/silver/theme'
import 'tinymce/plugins/link'
import 'tinymce/plugins/image'
import 'tinymce/plugins/media'
import 'tinymce/plugins/table'
import 'tinymce/plugins/lists'
import 'tinymce/plugins/wordcount'
import 'tinymce/plugins/fullpage'
import 'tinymce/plugins/preview'
import 'tinymce/plugins/print'
import 'tinymce/plugins/hr'
import 'tinymce/plugins/fullscreen'
import 'tinymce/plugins/emoticons'
import 'tinymce/plugins/anchor'
import 'tinymce/plugins/help'
import 'tinymce/plugins/searchreplace'
import 'tinymce/plugins/insertdatetime'
// import 'tinymce/plugins/autosave'

export default {
  components: {
    Editor
  },
  props: {
    //传入一个value，使组件支持v-model绑定
    value: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    plugins: {
      type: [String, Array],
      default: 'link image media table lists wordcount fullpage preview print hr fullscreen emoticons anchor help searchreplace insertdatetime'
    },
    toolbar: {
      type: [String, Array],
      default: 'undo redo |  formatselect | fontsizeselect | fontselect | bold italic underline strikethrough hr subscript superscript link forecolor backcolor emoticons | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | image media table wordcount anchor | removeformat searchreplace insertdatetime preview print fullscreen help custom-button'
    }
  },
  data() {
    return {
      //初始化配置
      init: {
        language: 'zh_CN',
        language_url: 'tinymce/zh_CN.js',
        skin_url: 'tinymce/skins/ui/oxide',
        emoticons_database_url: 'tinymce/emojis.js',
        height: 350,
        plugins: this.plugins,
        toolbar: this.toolbar,
        // menubar: true,
        // menubar: 'file edit insert view format table tools help',
        branding: false, //去除右下角的'由tinymce驱动'
        elementpath: false, //左下角的当前标签路径
        // autosave_interval: '10s',
        content_css: 'tinymce/skins/content/default/content.css', //对编辑器内部需要的一些样式
        fullpage_default_font_size: "14px",
        fontsize_formats: '11px 12px 14px 16px 18px 24px 36px 48px',
        font_formats: '宋体; 微软雅黑; 楷体; 黑体; 隶书; Arial; Courier New; Georgia; Serif; Times New Roman',
        fullpage_default_font_family: 'Arial',
        //此处为图片上传处理函数，这个直接用了base64的图片形式上传图片，
        //如需ajax上传可参考https://www.tiny.cloud/docs/configure/file-image-upload/#images_upload_handler
        images_upload_handler: (blobInfo, success, failure) => {
          const img = 'data:image/jpeg;base64,' + blobInfo.base64();
          success(img);
        },
        //设置自定义功能的按钮
        setup: editor => {
          editor.ui.registry.addButton('custom-button', {
            tooltip: '自定义按钮',
            // text: '自定义按钮',
            onAction: () => {},
            icon: 'custom'
          });
          editor.ui.registry.addMenuItem('codeformat', {
            text: 'Code',
            icon: 'sourcecode',
            onAction: () => {}
          });
        },
        init_instance_callback: function(editor) {
          tinymce.dom.DomQuery('button[title="自定义按钮"] svg').remove();
          tinymce.dom.DomQuery('button[title="自定义按钮"]').css('background', `url(${ require('@/assets/cookie.png') }) no-repeat center center / 24px 24px`);
        }
      },
      myValue: this.value
    }
  },
  methods: {
    change(e) {
      this.$emit('change', e, tinymce);
    },
    blur(e) {
      this.$emit('blur', e, tinymce);
    },
    clear() {
      this.myValue = '';
    }
  },
  watch: {
    value(newValue) {
      this.myValue = newValue;
    },
    myValue(newValue) {
      this.$emit('input', newValue);
    }
  }
}
</script>
<style scoped>
</style>