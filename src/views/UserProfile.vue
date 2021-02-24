<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>
      <CreateTwaatPanel @add-twaat="state.addTwaat" />
    </div>
    <div class="user-profile__twaats-wrapper">
      <TwaatItem
        v-for="twaat in state.user.twaats"
        :key="twaat.id"
        :username="state.user.username"
        :twaat="twaat"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwaatItem from "../components/TwaatItem";
import CreateTwaatPanel from "../components/reateTwaatPanel";
import { useRoute } from "vue-router";
import { users } from "../assets/users";
import { reactive, computed } from "vue";

export default {
  name: "UserProfile",
  components: { TwaatItem, CreateTwaatPanel },
  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0]
    });

    const addTwaat = (twaat) => {
      this.user.twaats.unshift({
        id: state.user.twaats.length + 1,
        content: twaat
      });
    };
    return {
      state,
      addTwaat,
      userId
    };
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/variables.scss";

.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #dfe3eb;

    h1 {
      margin: 0;
    }
    .user-profile__admin-badge {
      background: $main-color;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
    .user-profile__create-twaat {
      display: flex;
      flex-direction: column;
      padding-top: 20px;

      &.--exceeded {
        color: red;
        border-color: red;
      }
      &.--almost-exceeded {
        color: yellow;
        border-collapse: yellow;
      }
    }
  }
}
</style>
