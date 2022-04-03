<template>
  <section>
    <ul>
      <slot></slot>
    </ul>
  </section>
</template>

<script>
export default {
  name: "ui-layout-grid"
}
</script>

<style scoped>
  ul{
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    flex-wrap: wrap;
    padding: 0;

    list-style-type: none;
  }

  li{
    width: calc(100% / 3);
    padding: 2em;

    box-sizing: border-box;
  }
</style>
