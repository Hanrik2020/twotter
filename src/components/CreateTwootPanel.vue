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
    <textarea id="newTwoot" rows="4" v-model="state.newTwootContent" />

    <div class="create-twoot__twoot-type">
      <div>
        <label for="newTwootType"><strong>Type: </strong></label>

        <select
          class="create-twoot__twoot-selector"
          id="newTwootType"
          v-model="state.selectedTwootType"
        >
          <option
            :value="option.value"
            v-for="(option, index) in state.twootTypes"
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
    </div>
  </form>
</template>

<script>
import { reactive, computed } from "vue";

export default {
  name: "CreateTwootPanel",

  setup(props, ctx) {
    const state = reactive({
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
    });

    const newTwootCharacterCount = computed(() => state.newTwootContent.length);

    function createNewTwoot() {
      if (state.newTwootContent && state.selectedTwootType !== "draft") {
        ctx.emit("add-twoot", state.newTwootContent);
        state.newTwootContent = "";
      }
    }

    return {
      state,
      newTwootCharacterCount,
      createNewTwoot,
    };
  },
};
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  margin-right: 50px;

  #newTwoot {
    border-radius: 5px;
  }

  .create-twoot__twoot-type {
    padding: 10px 0;
    display: flex;
    justify-content: space-between;
  }

  .create-twoot__twoot-selector {
    margin: 5px 0;
  }

  .create-twoot__twoot-button {
    border-radius: 5px;
    background-color: cornflowerblue;
    color: white;
    border: 2px solid cornflowerblue;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.1s ease;
    &.--exceeded {
      display: none;
    }
    &:hover {
      background-color: lightgreen;
      color: black;
      transform: scale(1.1, 1.1);
    }
  }
  .create-twoot__twoot-label {
    &.--exceeded {
      color: red;
    }
  }
}
</style>