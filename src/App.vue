<template>
  <div id="app">
    <nav>
      <div class="navigation-logo">Twotter</div>
      <div class="navigation-user">@{{ user.username }}</div>
    </nav>
    <div class="app-content">
      <UserProfile />
    </div>
  </div>
</template>
  

<script>
import UserProfile from "./components/UserProfile";

export default {
  name: "App",
  components: { UserProfile },
  data() {
    return {
      user: {
        username: "hankenbrune",
      },
    };
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Fredoka+One&display=swap");
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
nav {
  display: flex;

  align-items: center;
  color: whitesmoke;
  height: 4rem;
  background-color: cornflowerblue;
  margin-bottom: 3rem;

  .navigation-logo {
    display: flex;
    align-items: center;
    margin-left: 3rem;
    font-family: "Fredoka One", cursive;
    font-size: 2rem;
    font-weight: bolder;
    text-align: center;
    letter-spacing: 2px;
  }
  .navigation-user {
    font-weight: 600;
    margin-left: auto;
    padding-right: 3rem;
    font-size: 1.1rem;
  }
}
</style>
