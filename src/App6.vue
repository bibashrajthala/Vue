<template>
  <div>
    <div><CreatePost /></div>
    <div>
      <PostList />
    </div>

    <Parent />
  </div>
</template>

<script>
import PostList from "./components/PostList.vue";
import CreatePost from "./components/CreatePost.vue";
import Parent from "./components/Parent.vue";

export default {
  name: "App",
  components: {
    PostList,
    CreatePost,
    Parent,
  },
};
</script>

<style scoped></style>
