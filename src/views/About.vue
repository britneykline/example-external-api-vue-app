<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  created: function () {
    var githubAccessToken = localStorage.getItem('github_access_token');
    if (githubAccessToken) {
      axios
        .get("/github_profile?github_access_token=" + githubAccessToken)
        .then((response) => {
          console.log(response.data);
        });
    }
  },
};
</script>