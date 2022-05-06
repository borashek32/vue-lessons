<template>
  <div>
    <input 
      class="input" 
      type="text"
      :value="modelValue"
      @input="updateInput"
    >
  </div>
</template>

<script>
export default {
  name: 'my-input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
.input {
  width: 80%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-bottom: 15px;
}
</style>