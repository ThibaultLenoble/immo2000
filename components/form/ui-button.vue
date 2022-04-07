<template>
  <div>
    <button :type="type">{{ label }}</button>
  </div>
</template>

<script>
export default {
  name: "ui-button",
  props: {
    type: String,
    label: String
  }
}
</script>

<style scoped>

</style>
