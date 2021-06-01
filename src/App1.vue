<template>
  <div id="app">
<!--    <ImageEditor />-->
    <imageMosaic/>
  </div>
</template>
<script>

// import ImageEditor from "./components/ImageEditor";
import imageMosaic from "./components/imageMosaic";
export default {
  components: {
    // ImageEditor,
    imageMosaic
  }
}
</script>

<style lang="scss">
.page {
  padding: 20px;
}
button,
.btn.btn-primary {
  margin-right: 10px !important;
}
.button-toolbar {
  margin-bottom: 10px;
}
</style>