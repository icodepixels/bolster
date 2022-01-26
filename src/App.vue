<template>
  <div id="app">
    <Profile />
  </div>
</template>

<style>
  @import './App.css';
</style>

<script>
import Profile from "./views/Profile.vue";

export default {
  name: "App",
  components: {
    Profile
  }
};
</script>
