<template>
  <div id="app">
    <div class="header">Twotter <img src="./assets/img/birb.png" /></div>

    <UserProfile />
  </div>
</template>
  

<script>
import UserProfile from "./components/UserProfile";

export default {
  name: "App",
  components: { UserProfile },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Fredoka+One&display=swap");
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 30px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Fredoka One", cursive;
  font-size: 4rem;
  font-weight: bolder;
  text-align: center;
  margin: 20px 0;
}

.header img {
  width: 10%;
}
</style>
