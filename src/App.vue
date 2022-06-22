<template>
  <div>
    <git-hub-pulls :owner="'mailhog'" :repo="'MailHog'"></git-hub-pulls>
  </div>
</template>

<script>
import GitHubPulls from "./components/GitHubPulls";
export default {
  name: "App",
  components: {
    GitHubPulls,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
