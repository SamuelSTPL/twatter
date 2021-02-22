<template>
  <form
    class="create-twaat-panel"
    @submit.prevent="createNewTwaat"
    :class="{
      '--exceeded': newTwaatCharactersCount > 180,
      '--almost-exceeded':
        newTwaatCharactersCount > 150 && newTwaatCharactersCount < 180
    }"
  >
    <label for="newTwaat">
      <strong>New Twaat</strong>
      ({{ newTwaatCharactersCount }}/180)
    </label>
    <textarea id="newTwaat" rows="4" v-model="state.newTwaatContent" />

    <div class="create-twaat-panel__submit">
      <div class="create-twaat-type">
        <label for="newTwaatType"><strong>Type:</strong></label>
        <select id="newTwaatType" v-model="state.newTwaatType">
          <option
            :value="option.value"
            v-for="(option, index) in state.twaatTypes"
            :key="index"
          >
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>
        Twaat it!
      </button>
    </div>
  </form>
</template>

<script>
import { reactive, computed } from "vue";

export default {
  name: "CreateTwaatPanel",

  setup(props, ctx) {
    const state = reactive({
      newTwaatContent: "",
      newTwaatType: "instant",
      twaatTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twaat" }
      ]
    });
    // Will return the amount of characters
    const newTwaatCharactersCount = computed(
      () => state.newTwaatContent.length
    );

    const createNewTwaat = () => {
      if (state.newTwaatContent && state.newTwaatType !== "draft") {
        ctx.emit("add-twaat", state.newTwaatContent);
        state.newTwaatContent = "";
      }
    };

    return {
      state,
      newTwaatCharactersCount,
      createNewTwaat
    };
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/variables.scss";

.create-twaat-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }
  .create-twaat-panel__submit {
    display: flex;
    justify-content: space-between;
    .create-twoot-type {
      padding: 10px 0;
    }
    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: $main-color;
      color: white;
      font-weight: bold;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
  }
  &.--almost-exceeded {
    color: yellow;
    border-collapse: yellow;
  }
}
</style>
