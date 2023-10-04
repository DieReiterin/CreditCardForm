<template>
    <label class="form__block-title"><slot></slot></label>
</template>
<script>
export default {
    name: 'my-title'
}
</script>
<style scoped>
.form__block-title {
  display: block;
  width: 100%;
  margin-bottom: 5px;
  font-size: 14px;
  font-weight: 500;
  color: #1a3b5d;
}
</style>