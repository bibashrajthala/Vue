<template>
  <input type="text" :value="modelValue" @input="$emit('update:modelValue')" />
</template>

<script>
export default {
  name: "Input",
  props: {
    modelValue: String,
  },
};
</script>

<style></style>
