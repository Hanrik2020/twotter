<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-prifle__follower-count">
        <strong>Followers: {{ followers }}</strong>
      </div>

      <form
        class="user-profile__create-twoot"
        v-on:submit.prevent="createNewTwoot"
      >
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent" />

        <div class="user-profile__create-twoot-type">
          <label for="newTwootType"><strong>Type</strong></label>
          <select
            class="user-profile__twoot-selector"
            id="newTwootType"
            v-model="selectedTwootType"
          >
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>Twoot!</button>
      </form>
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

export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
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
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log(`Favorited twoot #${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.user.twoot.unshift({
          id: this.user.twoot.length + 1,
          content: this.newTwootContent,
          isFavorite: false,
        });
      }
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 70%;
  padding: 50px 5%;
  margin: auto;
  background-color: cornflowerblue;
  border-radius: 5px;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile__admin-badge {
  background-color: rebeccapurple;
  border-radius: 5px;
  padding: 3px 5px;
  color: white;
  margin-right: auto;
  font-weight: 600;
}

.user-profile__create-twoot {
  display: flex;
  flex-direction: column;

  padding-top: 20px;
}

.user-profile__twoot-selector {
  margin: 5px 0;
}

.user-profile__create-twoot-type {
  padding-bottom: 10px;
}

h1 {
  margin: 0;
}
</style>
