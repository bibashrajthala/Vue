<template>
  <form @submit.prevent="createPost">
    <div>
      <label for="userId">User id</label>
      <input type="number" id="userId" v-model="formData.userId" />
    </div>
    <div>
      <label for="title">Title</label>
      <input type="text" id="title" v-model="formData.title" />
    </div>
    <div>
      <label for="body">Body</label>
      <input type="text" id="body" v-model="formData.body" />
    </div>

    <button type="submit">Submit</button>
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "CreatePost",
  data() {
    return {
      formData: {
        userId: "",
        title: "",
        body: "",
      },
    };
  },
  methods: {
    async createPost() {
      try {
        await axios.post(
          "https://jsonplaceholder.typicode.com/posts",
          this.formData
        );
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped></style>
