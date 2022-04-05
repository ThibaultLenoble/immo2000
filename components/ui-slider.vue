<template>
  <div>
    <ul>
      <slot></slot>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ui-slider"
}
</script>

<style scoped>
  ul{
    display: flex;
    flex-direction: row;
    list-style-type: none;
    padding: 0;
  }

  li {
    width: 400px;
    height: 300px;
  }

  li img{
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
</style>
