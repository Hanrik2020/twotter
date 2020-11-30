<template>
  <div class="user-profile">
    <div
      class="user-profile__user-panel"
      :class="{ '--exceeded': newTwootCharacterCount > 180 }"
    >
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-prifle__follower-count">
        <strong>Followers: {{ followers }}</strong>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoot"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>
  

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";

export default {
  name: "UserProfile",
  components: { TwootItem, CreateTwootPanel },
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

        twoot: [
          { id: 1, content: "Hej hej halloe", isFavorite: false },
          { id: 2, content: "Don't eat humans.", isFavorite: false },
        ],
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
  computed: {},

  methods: {
    addTwoot(twoot) {
      this.user.twoot.unshift({
        id: this.user.twoot.length + 1,
        content: twoot,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 70%;
  padding: 50px 5%;
  margin: auto;
  background-color: cornflowerblue;
  border-radius: 5px;

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
