<template>
  <div>
    <h4>From child</h4>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "ChildStyles",
};
</script>

<style scoped>
h4 {
  color: green;
}
</style>
