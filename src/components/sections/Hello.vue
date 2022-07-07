<template>
<h1>Ya tebya lublu</h1>
  <Button :button-text="tempData['button-text']"/>
</template>

<script>
import tempData from "../../tempData/tempData.json"
import Button from "@/components/button/Button";
export default {
  name: "HelloWorld",
  components: {
    Button,
  },
  data() {
    return {
      tempData
    }
  }
}
</script>

<style lang="scss">
@import "../../assets/styles/hello";
</style>