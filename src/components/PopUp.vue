<template>
  <div>
    Hello from popup

    <input type="text" placeholder="Enter name" v-model="name" />

    <button @click="$emit('close', name)">Close Popup</button>
  </div>
</template>

<script>
export default {
  name: "PopUp",
  data() {
    return {
      name: "",
    };
  },
  //   emits: ["close"],

  //   Validating emited events
  emits: {
    close(name) {
      return !!name; // its like validation, true means validated, and false(empty name) means not validated in console warning
    },
  },
};
</script>

<style></style>
