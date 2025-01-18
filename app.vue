<template>
  <div>
    <ClientOnly>
      <Editor v-model="content" tinymceScriptSrc="tinymce/tinymce.min.js" :init="init" />
      <div>
        <p>CONTENT:</p>
        <p>{{ content }}</p>
      </div>
    </ClientOnly>
  </div>
</template>

<script setup>
import Editor from '@tinymce/tinymce-vue'

const Theme = false
const content = ref("")
const init = {
  license_key: 'gpl',
  plugins: 'accordion advlist anchor autolink autosave charmap code codesample directionality emoticons fullscreen help image importcss insertdatetime link lists media nonbreaking pagebreak preview save searchreplace table quickbars visualchars wordcount visualblocks',
  menubar: 'edit view insert format tools table tc help',
  toolbar: "undo redo | importword exportword exportpdf | revisionhistory | aidialog aishortcuts | blocks fontsizeinput | bold italic | align numlist bullist | link image | table math media pageembed | lineheight  outdent indent | strikethrough forecolor backcolor formatpainter removeformat | charmap emoticons checklist | code fullscreen preview | save print | pagebreak anchor codesample footnotes mergetags | addtemplate inserttemplate | addcomment showcomments | ltr rtl casechange | spellcheckdialog a11ycheck", // Note: if a toolbar item requires a plugin, the item will not present in the toolbar if the plugin is not also loaded.
  quickbars_selection_toolbar: 'bold italic | quicklink h2 h3 blockquote quickimage quicktable',
  contextmenu: 'link image editimage table configurepermanentpen',
  noneditable_class: 'mceNonEditable',
  toolbar_mode: 'sliding',
  tinycomments_mode: 'embedded',
  content_style: '.mymention{ color: gray; }',
  skin: Theme ? 'oxide-dark' : 'oxide',
  content_css: Theme ? 'dark' : 'default',
  autocorrect_capitalize: true,
  a11y_advanced_options: true,
  image_advtab: true,
  importcss_append: true,
  height: 700,
  image_caption: true,
  editimage_cors_hosts: ['picsum.photos'],
  exportpdf_converter_options: {
    'format': 'Letter',
    'margin_top': '1in',
    'margin_right': '1in',
    'margin_bottom': '1in',
    'margin_left': '1in'
  },
  exportword_converter_options: {
    'document': {
      'size': 'Letter'
    }
  },
  importword_converter_options: {
    'formatting': {
      'styles': 'inline',
      'resets': 'inline',
      'defaults': 'inline',
    }
  },
  file_picker_callback: (callback, value, meta) => {
    /* Provide file and text for the link dialog */
    if (meta.filetype === 'file') {
      callback('https://www.google.com/logos/google.jpg', { text: 'My text' });
    }

    /* Provide image and alt text for the image dialog */
    if (meta.filetype === 'image') {
      callback('https://www.google.com/logos/google.jpg', { alt: 'My alt text' });
    }

    /* Provide alternative source and posted for the media dialog */
    if (meta.filetype === 'media') {
      callback('movie.mp4', { source2: 'alt.ogg', poster: 'https://www.google.com/logos/google.jpg' });
    }
  },
  // typography_ignore: ['code'],
  // typography_rules: [
  //     'common/punctuation/quote',
  //     'en-US/dash/main',
  //     'common/nbsp/afterParagraphMark',
  //     'common/nbsp/afterSectionMark',
  //     'common/nbsp/afterShortWord',
  //     'common/nbsp/beforeShortLastNumber',
  //     'common/nbsp/beforeShortLastWord',
  //     'common/nbsp/dpi',
  //     'common/punctuation/apostrophe',
  //     'common/space/delBeforePunctuation',
  //     'common/space/afterComma',
  //     'common/space/afterColon',
  //     'common/space/afterExclamationMark',
  //     'common/space/afterQuestionMark',
  //     'common/space/afterSemicolon',
  //     'common/space/beforeBracket',
  //     'common/space/bracket',
  //     'common/space/delBeforeDot',
  //     'common/space/squareBracket',
  //     'common/number/mathSigns',
  //     'common/number/times',
  //     'common/number/fraction',
  //     'common/symbols/arrow',
  //     'common/symbols/cf',
  //     'common/symbols/copy',
  //     'common/punctuation/delDoublePunctuation',
  //     'common/punctuation/hellip'
  // ],
}
</script>