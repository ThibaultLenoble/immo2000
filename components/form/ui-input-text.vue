<template>
  <div>
    <label :for="id">{{ label }}</label>
    <input v-model="inputValue" :type="type" :name="name" :placeholder="placeholder" :id="id" @input="handleInput">
  </div>
</template>

<script>
export default {
  name: "ui-input-text",
  props: {
    id: String,
    name: String,
    label: String,
    type: String,
    placeholder: String,
  },
  data(){
    return {
      inputValue : this.inputValue
    }
  },
  methods: {
    handleInput (e) {
      this.$emit('input', this.$data.inputValue)
    }
  }
}
</script>

<style scoped>

</style>
