<template>
  <form
    class="create-twoot-panel"
    v-on:submit.prevent="createNewTwoot"
    :class="{ '--exceeded': newTwootCharacterCount > 180 }"
  >
    <label
      class="create-twoot__twoot-label"
      :class="{ '--exceeded': newTwootCharacterCount > 180 }"
      for="newTwoot"
      ><strong>New Twoot </strong>({{ newTwootCharacterCount }}/180)</label
    >
    <textarea id="newTwoot" rows="4" v-model="newTwootContent" />

    <div class="create-twoot__twoot-type">
      <label for="newTwootType"><strong>Type</strong></label>
      <select
        class="create-twoot__twoot-selector"
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
    <button
      class="create-twoot__twoot-button"
      :class="{ '--exceeded': newTwootCharacterCount > 180 }"
    >
      Twoot!
    </button>
  </form>
</template>

<script>
export default {
  name: "CreateTwootPanel",
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
    };
  },
  computed: {
    newTwootCharacterCount() {
      return this.newTwootContent.length;
    },
  },
  methods: {
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.$emit("add-twoot", this.newTwootContent);
        this.newTwootContent = "";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  display: flex;
  flex-direction: column;
  padding-top: 20px;

  .create-twoot__twoot-type {
    padding-bottom: 10px;
  }

  .create-twoot__twoot-selector {
    margin: 5px 0;
  }

  .create-twoot__twoot-button {
    &.--exceeded {
      display: none;
    }
  }
  .create-twoot__twoot-label {
    &.--exceeded {
      color: red;
    }
  }
}
</style>