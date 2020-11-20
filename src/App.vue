<template>
  <div id="app">
    @{{ user.username }} - {{ fullName }}
    <strong>Followers: {{ followers }}</strong>
    <button v-on:click="followUser">Follow</button>
  </div>
</template>
  

<script>
export default {
  name: "App",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "hankenbrune",
        firstName: "Henrik",
        lastName: "Rydstrom",
        email: "henrik.rydstrom@gmail.com",
        isAdmin: true,
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} just gained a new follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 30px;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
}
</style>
