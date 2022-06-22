<template>
  <div>
    <table v-if="errorHasOccurred === false">
      <thead>
        <tr>
          <th>Number</th>
          <th>Title</th>
          <th>User</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pull, index) in pullRequests" :key="index">
          <td>{{ pull.number }}</td>
          <td>{{ pull.title }}</td>
          <td>{{ pull.user.login }}</td>
        </tr>
      </tbody>
    </table>

    <div v-else>
      Opps something went wrong there, try again?
      <button @click="retryPulls">Again!</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "GitHubPulls",
  data() {
    return {
      errorHasOccurred: false,
      pullRequests: [],
    };
  },
  computed: {
    pullUri() {
      // return "https://www.gov.uk/bank-holidays.json";
      return `https://api.github.com/repos/${this.owner}/${this.repo}/pulls`;
    },
  },
  mounted() {
    this.getPullRequests();
  },
  methods: {
    async getPullRequests() {
      const response = await fetch(this.pullUri, {
        headers: {
          Accept: "application/vnd.github.v3+json",
        },
      });
      if (!response.ok) {
        this.errorHasOccurred = true;
        return;
      }

      this.pullRequests = await response.json();
    },
    retryPulls() {
      this.errorHasOccurred = false;
      this.getPullRequests();
    },
  },
  props: {
    repo: String,
    owner: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
