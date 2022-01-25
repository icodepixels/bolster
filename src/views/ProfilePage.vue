<template>
  <div class="ProfilePage">
    <p v-if="!profile">Loading...</p>
    <div class="ProfilePage__container fade-in-image" v-if="profile">
      <v-author :name="profile.name" :bio="profile.bio" :picture="profile.picture" />
      <div class="ProfilePage__experience">
        <v-experience
          v-for="experience in profile.experience"
          v-bind:experience="experience"
          v-bind:index="experience.id"
          v-bind:key="experience.id"
        />
        <div class="ProfilePage__actionsContainer">
          <component
            v-bind:is="componentForm"
            :handleClose="handleClose"
            :handleSubmit="handleSubmit"
          />
          <div class="ProfilePage__actions">
            <v-button
              :onClick="handleClick"
              class="ProfilePage__button"
              v-bind:buttonTitle="buttonTitle"
              v-bind:buttonClass="buttonClass"
              v-bind:is="buttonExperience"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.fade-in-image {
  animation: fadeIn 2s;
}
@keyframes fadeIn {
  0% {opacity:0;}
  100% {opacity:1;}
}
.ProfilePage {
}
.ProfilePage__container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  margin: auto;
  max-width: 1024px;
}
.ProfilePage__experience {
  display: flex;
  flex-direction: column;
  max-width: 500px;
}
.ProfilePage__actions {
  display: flex;
}
.ProfilePage__actionsContainer {
  margin: 24px 0;
  padding: 0 16px;
}
.ProfilePage__button {
  max-width: 300px;
}
</style>

<script>
import axios from "axios";
import Author from "../components/Author.vue";
import Button from '../components/Button';
import Experience from "../components/Experience";
import ExperienceForm from "../components/ExperienceForm";

export default {
  name: "ProfilePage",
  data: function () {
    return {
      buttonTitle: "Add Experience",
      buttonClass: "Button",
      componentCloseForm: null,
      componentForm: null,
      buttonExperience: 'v-button',
      profile: {}
    }
  },
  components: {
    'v-author': Author,
    'v-button': Button,
    'v-experience': Experience,
    'v-experience-form': ExperienceForm,
  },
  methods: {
    handleClick: function () {
      if (this.componentForm !== 'v-experience-form') {
        this.componentForm = 'v-experience-form';
        this.buttonExperience = null;
        setTimeout(() => document.getElementById("company").focus(), 50);
      }
    },
    handleClose: function () {
      if (this.componentForm === 'v-experience-form') {
        this.componentForm = null;
        this.buttonExperience = 'v-button';
      }
    },
    handleSubmit: function (newExperience) {
      this.profile.experience.push(newExperience);
      this.handleClose();
    }
  },
  async mounted() {
    let res = await axios.get("/api/profile");
    this.profile = res.data.length > 0 ? res.data[0] : {};
  },
};
</script>
