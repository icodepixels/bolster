<template>
  <div class="Experience">
    <component
      v-bind:is="component"
      v-bind:experience="experience"
      :edit="handleClick"
      :buttonTitle="buttonTitle"
      :handleClose="handleClose"
      :handleSubmit="handleSubmit"
    />
  </div>
</template>

<style>
.Experience {
  border-bottom: 1px solid #81b247;
  padding: 16px;
}
.Experience:last-child {
  border-bottom: 0;
}
.Experience__companyContainer {
  display: flex;
  justify-content: space-between;
}
.Experience__editBtn:hover {
  cursor: pointer;
  color: #1b240e;
  transition: color 0.3s ease-in;
}
.Experience__editBtn {
  background: transparent;
  border: 0;
  color: #81b247;
  outline: none;
}
.Experience__title {
  align-items: baseline;
  display: flex;
  justify-content: space-between;
}
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
