<template>
  <div class="Author">
    <img :src="this.picture" alt="picture" class="Author__picture" />
    <h3 class="Author__name">{{ this.name }}</h3>
    <div class="Author__bio">
      <span class="Author__bio--label">Background:</span>
      <p>{{ this.bio }}</p>
    </div>
  </div>
</template>

<style>
  @import './Author.css';
</style>

<script>
export default {
  props: {
    name: {
      type: String
    },
    bio: {
      type: String
    },
    picture: {
      type: String
    }
  },
  created() { }
}
</script>