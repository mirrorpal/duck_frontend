<template>
    <div class="layout-form">
      <div class="tips">
        <h2>富文本编辑器</h2>
      </div>
      <textarea class='tinymce-textarea' id="tinymceEditer"></textarea>
      <br>
      <Button type="primary" @click="getContent">获取内容</Button>
    </div>
</template>

<script>
    import tinymce from 'tinymce'
    export default {
      methods:{
        init(){
          this.$nextTick(() => {
            tinymce.init({
              selector: '#tinymceEditer',
              branding: false,
              elementpath: false,
              height: 400,
              language: 'zh_CN.GB2312',
              menubar: 'edit insert view format table tools',
              plugins: [
                'advlist autolink lists link image charmap print preview hr anchor pagebreak imagetools',
                'searchreplace visualblocks visualchars code fullpage',
                'insertdatetime media nonbreaking save table contextmenu directionality',
                'emoticons paste textcolor colorpicker textpattern imagetools codesample'
              ],
              toolbar1: ' newnote print preview | undo redo | insert | styleselect | forecolor backcolor bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | link image emoticons media codesample',
              autosave_interval: '20s',
              image_advtab: true,
              table_default_styles: {
                width: '100%',
                borderCollapse: 'collapse'
              },
              setup: function (editor) {
                editor.on('init', function (e) {
                  if (localStorage.editorContent) {
                    tinymce.get('tinymceEditer').setContent(localStorage.editorContent);
                  }
                });
                editor.on('keydown', function (e) {
                  localStorage.editorContent = tinymce.get('tinymceEditer').getContent();
                });
              }
            });
          });
        },
        getContent(){
          alert(tinymce.get('tinymceEditer').getBody().innerHTML);
        }
      },
      mounted () {
        this.init();
      },
      destroyed () {
        tinymce.get('tinymceEditer').destroy();
      }
    }
</script>

<style scoped>

</style>
