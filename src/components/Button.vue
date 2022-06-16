<template>
  <button class="btn" :style="{ background: btnColor, color: txtColor }">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    btnColor: String,
    txtColor: String,
  },
}
</script>

<style></style>
