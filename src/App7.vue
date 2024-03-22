<template>
  <!-- TEMPLATE REFS => just like refs of react js provided by useRef() -->
  <!-- when used in element provided reference to instance of that element but when
  used in component, gives reference to instance of that component(data,
  methods,etc) -->
  <div>
    <input type="text" ref="inputRef" />
    <PostList ref="postListRef" />
  </div>

  <!-- Mixins  -->
  <ClickCounter />
  <HoverCounter />
</template>

<script>
import PostList from "./components/PostList.vue";
import ClickCounter from "./components/ClickCounter.vue";
import HoverCounter from "./components/HoverCounter.vue";

export default {
  name: "App",
  components: {
    PostList,
    ClickCounter,
    HoverCounter,
  },
  mounted() {
    this.$refs.inputRef.focus();
    console.log("input ref", this.$refs.inputRef);
    console.log("post list ref", this.$refs.postListRef);
  },
};
</script>

<style scoped></style>
