<template>
  <div>
    <h2>{{ title }}</h2>
  </div>
</template>

<script>
export default {
  name: "ui-section-title",
  props: {
    title: {
      type: String,
    }
  }
}
</script>

<style scoped>
div {
  padding: 2em;
}
</style>
