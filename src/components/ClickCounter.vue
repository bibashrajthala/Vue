<template>
  <div>
    <button @click="increaseCounter">{{ count }} times clicked</button>
  </div>
</template>

<script>
import CounterMixin from "../mixins/counter";

export default {
  name: "ClickCounter",
  //   mixin can have any logic related codes like life cycle methods, or attribures like data , computed, watcher, methods, etc
  // if same thing is defined in component as well , it gets replaced / overridden by component, eg count of mixin of data() is overridden by count of component's data()
  mixins: [CounterMixin],
  data() {
    return {
      count: 100,
    };
  },
};
</script>

<style scoped></style>
