<template>
  <div class="app">
    <UserProfile />
  </div>
</template>

<script>
import { reactive } from "vue";
import UserProfile from "./components/UserProfile";

export default {
  name: "App",
  components: { UserProfile },
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
