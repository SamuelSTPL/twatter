<template>
  <div class="twaat-item" @click="favouriteTwaat(twaat.id)">
    <div class="user-profile__twaat">
      <div class="twaat-item__user">@{{ username }}</div>
      <div class="twaat-item__content">
        {{ twaat.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwaatItem",
  props: {
    username: {
      type: String,
      required: true
    },
    twaat: {
      type: Object,
      required: true
    }
  },
  methods: {
    favouriteTwaat(id) {
      this.$emit("favourite", id);
    }
  }
};
</script>

<style lang="scss" scoped>
.twaat-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  &:hover {
    transform: scale(1.1, 1.1);
  }
  .twaat-item__user {
    font-weight: bold;
  }
}
</style>
