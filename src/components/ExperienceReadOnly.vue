<template>
  <div class="ExperienceReadOnly fade-in-image">
    <div class="ExperienceReadOnly__companyContainer">
      <h4 class="ExperienceReadOnly__company">{{ experience.company }}</h4>
      <v-button
        :onClick="edit"
        class="ExperienceReadOnly__editBtn"
        :buttonTitle="buttonTitle"
        :buttonClass="buttonClass"
      />
    </div>
    <div class="ExperienceReadOnly__title">
      <h5>{{ experience.title }}</h5>
      <p>{{ experience.dates }}</p>
    </div>
    <p class="ExperienceReadOnly__description">{{ experience.description }}</p>
  </div>
</template>

<style>
  @import './ExperienceReadOnly.css';
</style>

<script>
import Button from './Button';
export default {
  name: "ExperienceReadOnly",
  components: {
    'v-button': Button,
  },
  data: function () {
    return {
      buttonTitle: "Edit",
      buttonClass: "Text"
    }
  },
  methods: {
  },
  props: {
    edit: {
      type: Function
    },
    experience: {
      type: Object,
      required: true
    },
  },
  beforeMount: function () {
    this.$nextTick(function () {
      if (this.experience.dates.length < 9) {
        this.experience.dates = this.experience.dates + 'current';
      }
    })
  }
};
</script>
