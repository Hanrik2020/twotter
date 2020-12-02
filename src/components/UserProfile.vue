<template>
  <div class="user-profile">
    <div class="user-profile__user-twoot">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ state.user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
        </div>

        <div class="user-prifle__follower-count">
          <strong>Followers: {{ state.followers }}</strong>
        </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>

    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>
  

<script>
import { reactive } from "vue";

import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";

export default {
  name: "UserProfile",
  components: { TwootItem, CreateTwootPanel },

  setup() {
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: "hankenbrune",
        firstName: "Henrik",
        lastName: "Rydstrom",
        email: "henrik.rydstrom@gmail.com",
        isAdmin: true,

        twoots: [
          { id: 1, content: "Hej hej halloe", isFavorite: false },
          { id: 2, content: "Don't eat humans.", isFavorite: false },
        ],
      },
    });

    function addTwoot(twoot) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: twoot,
      });
    }

    return {
      state,
      addTwoot,
    };
  },

  // watch: {
  //   followers(newFollowerCount, oldFollowerCount) {
  //     if (oldFollowerCount < newFollowerCount) {
  //       console.log(`${this.user.username} just gained a new follower!`);
  //     }
  //   },
  // },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px 5%;
  margin: 20px;
  background-color: lightsteelblue;
  border-radius: 15px;

  .user-profile__user-twoot {
    display: flex;
    flex-direction: column;
  }

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background-color: rebeccapurple;
      border-radius: 5px;
      padding: 3px 5px;
      color: white;
      margin-right: auto;
      font-weight: 600;
    }
  }
}
</style>
