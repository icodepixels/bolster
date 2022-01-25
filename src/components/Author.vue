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
.Author {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  max-width: 300px;
  padding: 16px;
}
.Author__picture {
  border-radius: 200px;
  width: 70%;
}
.Author__name {
  font-size: 1.5em;
  font-weight: bold;
  text-align: center;
}
.Author__bio {
  text-align: left;
}
.Author__bio--label {
  font-weight: bold;
  text-align: left;
}
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