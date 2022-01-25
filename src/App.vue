<template>
  <div id="app">
    <ProfilePage />
  </div>
</template>

<script>
import ProfilePage from "./views/ProfilePage.vue";

export default {
  name: "App",
  components: {
    ProfilePage
  }
};
</script>

<style>
@font-face {
  font-family: "RobotoMono Bold";
  src: local("RobotoMono Bold"),
    url(./fonts/RobotoMono/RobotoMono-Bold.ttf) format("truetype");
}
@font-face {
  font-family: "RobotoMono Light";
  src: local("RobotoMono Light"),
    url(./fonts/RobotoMono/RobotoMono-Light.ttf) format("truetype");
}
* {
  padding: 0;
  margin: 0;
}
body {
  font-family: "RobotoMono Light", Helvetica, Arial;
  color: #1b240e;
}
h1, h2, h3, h4, h5, h6 {
  font-family: "RobotoMono Bold", Helvetica, Arial;
  margin: 8px 0;
}
p {
  font-size: .82em;
  margin: 8px 0;
}
</style>
