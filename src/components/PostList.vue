<template>
  <div>
    <button @click="fetchPosts">Display posts</button>

    <div v-if="loading">loading...</div>
    <div v-if="!!errorMessage">{{ errorMessage }}</div>

    <div v-for="post in posts" :key="post.id">
      {{ post.id }} {{ post.title }}
      <p>{{ post.body }}</p>
      <hr />
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PostList",
  created() {
    this.fetchPosts();
  },
  data() {
    return {
      posts: [],
      errorMessage: "",
      loading: false,
    };
  },
  methods: {
    async fetchPosts() {
      try {
        this.loading = true;
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/posts"
        );
        this.posts = await res.data;
        this.loading = false;
      } catch (error) {
        console.log("error", error);
        this.errorMessage = "Failed to fetch posts";
        this.loading = false;
      }
    },
  },
};
</script>

<style scoped></style>
