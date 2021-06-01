const icona = require("tui-image-editor/dist/svg/icon-a.svg");
<template>
  <div class="page">
    <div class="imageEditorApp">
      <tui-image-editor ref="editor" :include-ui="useDefaultUI" :options="options"></tui-image-editor>
    </div>
  </div>
</template>
<script>
import { ImageEditor } from "@toast-ui/vue-image-editor";

export default {
  name: "ImageEditor",
  components: {
    "tui-image-editor": ImageEditor
  },
  data() {
    return {
      useDefaultUI: true,
      options: {
        includeUI: {
          loadImage: {
            path: 'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic26.nipic.com%2F20130115%2F8952533_013300701165_2.jpg&refer=http%3A%2F%2Fpic26.nipic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1625141261&t=58fa8a2e8eb2e0549a6fe10c481d3faa',
            name: 'SampleImage',
          },
          initMenu: 'filter',
          menuBarPosition: 'bottom',
        },
        cssMaxWidth: window.innerWidth,
        cssHeight: 800,
        initMenu: "filter"
      }
    };
  },   
};
</script>
<style scoped>
.imageEditorApp {
  width: 95vw;
  height: 95vh;
}

.tui-image-editor-header-logo{
  display: none;
}
</style>