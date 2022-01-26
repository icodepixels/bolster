<template>
  <div class="Experience">
    <component
      :is="component"
      :experience="experience"
      :edit="handleClick"
      :buttonTitle="buttonTitle"
      :handleClose="handleClose"
      :handleSubmit="handleSubmit"
    />
  </div>
</template>

<style>
  @import './Experience.css';
</style>

<script>
import axios from "axios";
import Button from './Button';
import ExperienceForm from "./ExperienceForm";
import ExperienceReadOnly from "./ExperienceReadOnly";

export default {
  name: "Experience",
  data: function () {
    return {
      buttonTitle: "Edit",
      buttonClass: "Text",
      componentCloseForm: null,
      component: 'v-experience-read-only',
    }
  },
  components: {
    'v-button': Button,
    'v-experience-form': ExperienceForm,
    'v-experience-read-only': ExperienceReadOnly,
  },
  methods: {
    handleClick: function () {
      if (this.component === 'v-experience-read-only') {
        this.component = 'v-experience-form';
        setTimeout(() => document.getElementById("company").focus(), 50);
      }
    },
    handleClose: function () {
      if (this.component === 'v-experience-form') {
        this.component = 'v-experience-read-only';
      }
    },
    async handleSubmit() {
        let res = await axios.post("/api/profile", this.experience);
        this.profile = res.data.length > 0 ? res.data[0] : {};
        this.component = 'v-experience-read-only';
    },
  },
  props: {
    experience: {
      type: Object,
      required: true
    },
  }
};
</script>
