<template>
  <div class="Profile">
    <p v-if="!profile">Loading...</p>
    <div class="Profile__container fade-in-image" v-if="profile">
      <v-author :name="profile.name" :bio="profile.bio" :picture="profile.picture" />
      <div class="Profile__experience">
        <v-experience
          v-for="experience in profile.experience"
          :experience="experience"
          :index="experience.id"
          :key="experience.id"
        />
        <div class="Profile__actionsContainer">
          <component
            :is="componentForm"
            :handleClose="handleClose"
            :handleSubmit="handleSubmit"
          />
          <div class="Profile__actions">
            <v-button
              class="Profile__button"
              :onClick="handleClick"
              :buttonTitle="buttonTitle"
              :buttonClass="buttonClass"
              :is="buttonExperience"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
  @import './Profile.css';
</style>

<script>
import axios from "axios";
import Author from "../components/Author.vue";
import Button from '../components/Button';
import Experience from "../components/Experience";
import ExperienceForm from "../components/ExperienceForm";

export default {
  name: "Profile",
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
