<template>
  <div class="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">Twatter</div>
      </router-link>
      <div class="navigation__user">{{ state.user.username }}</div>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
import { reactive } from "vue";

export default {
  name: "App",
  setup() {
    const state = reactive({
      user: {
        username: "_ZaFag"
      }
    });
    return {
      state
    };
  }
};
</script>

<style lang="scss">
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}
</style>
