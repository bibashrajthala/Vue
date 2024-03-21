<template>
  <div>
    <h2 @mouseover="increaseCounter">{{ count }} times hovered</h2>
  </div>
</template>

<script>
import CounterMixin from "../mixins/counter";

export default {
  name: "HoverCounter",
  mixins: [CounterMixin],
};
</script>

<style scoped></style>
