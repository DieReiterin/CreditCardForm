<template>
  <div class="container">
    <my-form></my-form>
  </div>

</template>

<script>
import MyForm from '@/components/MyForm.vue'

export default {
  name: 'App',
  components: {
    MyForm,
  }
}
</script>

<style>
@font-face {
  font-family: "SourceSans3";
  src: url(../src/fonts/SourceSans3-Medium.ttf);
}
:root {
  --main_color: rgb(118, 86, 178);
  --secondary_color: rgb(63, 40, 108);
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "SourceSans3", Arial, Helvetica, sans-serif;
}
.container {
  min-height: 100vh;                      
  display: flex;
  padding: 0px 15px;
  background-color: var(--main_color);
}

</style>
