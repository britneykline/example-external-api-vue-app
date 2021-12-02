<template>
  <div class="home">
    <a href="https://github.com/login/oauth/authorize?client_id=b515d8f5880ca01d42f8">Sign into GitHub</a>
    <div v-for="post in posts">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </div>
    <h1>{{ message }}</h1>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
    };
  },
  created: function () {
    axios.get("https://jsonplaceholder.typicode.com/posts").then((response) => {
      console.log(response.data);
      this.posts = response.data;
    });
    axios.get("/headlines").then((response) => {
      console.log("newsapi", response.data);
    });
    var code = this.$route.query.code;
    if (code) {
      axios.get("/auth/github/callback?code=" + code).then((response) => {
        localStorage.setItem("github_access_token", response.data.access_token);
        this.$router.push("/about");
      });
    }
  },
  methods: {},
};
</script>