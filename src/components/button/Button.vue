<template>
  <a href="" class="gradient-button"> {{ buttonText }}</a>
</template>

<script>
export default {
  name: "defaultButton",
  props: {
    buttonText: String,
  },
}
</script>

<style lang="scss">
@import "src/assets/styles/button";
</style>