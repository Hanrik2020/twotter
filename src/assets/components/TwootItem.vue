<template>
  <div class="twoot-item" @click="favoriteTwoot(twoot.id)">
    <div class="user-profile__twoot">
      <div class="twoot-item__user">@{{ username }}</div>
      <div class="twoot-item__content">
        {{ twoot.content }}
        <strong class="fav" v-if="twoot.isFavorite">Favorite</strong>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favoriteTwoot(id) {
      let twootItem = this.twoot;
      twootItem.isFavorite = !twootItem.isFavorite;
      this.$emit("favorite", id);
    },
  },
};
</script>

<style scoped>
.twoot-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin: 10px 0;
  margin-right: auto;
}

.twoot-item:hover {
  transform: scale(1.02, 1.02);
}

.twoot-item__user {
  font-weight: 600;
}

.fav {
  color: green;
}
</style>