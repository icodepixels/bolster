<template>
  <form class="ExperienceForm">
    <input
      type="text"
      placeholder="company"
      class="ExperienceForm__input"
      id="company"
      v-model="experience.company"
      name="company"
      :required="!experience.company"
    />
    <div
      v-if="error && !experience.company"
      class="ExperienceForm__error"
      v-bind:key="this.errors.company"
    >{{ this.errors.company }}</div>
    <div class="ExperienceForm__title">
      <div>
        <input
          type="text"
          placeholder="title"
          class="ExperienceForm__input"
          id="title"
          v-model="experience.title"
          name="title"
          :required="!experience.title"
        />
        <div
          v-if="error && !experience.title"
          class="ExperienceForm__error"
          v-bind:key="this.errors.title"
        >{{ this.errors.title }}</div>
      </div>
      <div>
        <input
          type="text"
          placeholder="dates"
          class="ExperienceForm__input"
          id="dates"
          v-model="experience.dates"
          name="dates"
          :required="!experience.dates"
        />
        <div
          v-if="error && !experience.dates"
          class="ExperienceForm__error"
          v-bind:key="this.errors.dates"
        >{{ this.errors.dates }}</div>
      </div>
    </div>
    <textarea
      type="text"
      placeholder="description"
      class="ExperienceForm__input ExperienceForm__textarea"
      id="description"
      v-model="experience.description"
      name="description"
      :required="!experience.description"
    />
    <div
      v-if="error && !experience.description"
      class="ExperienceForm__error"
      v-bind:key="this.errors.description"
    >{{ this.errors.description }}</div>

    <div v-if="errors.length" class="ExperienceForm__error">
      <span>Please correct the following error(s):</span>
      <ul class="ExperienceForm__error--list">
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
    </div>
    <div class="ExperienceForm__actions">
      <v-button
        :onClick="checkForm"
        class="ExperienceForm__button"
        v-bind:buttonTitle="buttonTitle"
        v-bind:buttonClass="buttonClass"
      />
      <v-button
        :onClick="handleClose"
        class="ExperienceForm__button"
        v-bind:buttonTitle="buttonCloseTitle"
        v-bind:buttonClass="buttonCloseClass"
      />
    </div>
  </form>
</template>

<style>
.ExperienceForm {
}
.ExperienceForm__actions {
  display: flex;
}
.ExperienceForm__button:first-child {
  margin-right: 16px;
}
.ExperienceForm__error {
  font-size: 0.7em;
  color: red;
  margin-bottom: 16px;
}
.ExperienceForm__title {
  align-items: baseline;
  display: flex;
  justify-content: space-between;
}
.ExperienceForm__input {
  padding: 8px;
  color: #1b240e;
  border: 1px solid #81b247;
  border-radius: 4px;
  margin: 8px 0;
  outline: none;
}
.ExperienceForm__input:error {
  border-color: red;
}
.ExperienceForm__input--error {
  border-color: red;
}
.ExperienceForm__textarea {
  width: 100%;
  max-width: 483px;
  min-height: 100px;
}
</style>

<script>
import Button from '../components/Button';

export default {
  name: "ExperienceForm",
  components: {
    'v-button': Button,
  },
  data: function () {
    return {
      buttonTitle: "Save",
      buttonCloseTitle: "Close",
      buttonClass: "Button",
      buttonCloseClass: "Button",
      errors: [],
      error: false
    }
  },
  props: {
    handleClose: {
      type: Function
    },
    handleSubmit: {
      type: Function
    },
    experience: {
      type: Object,
      default: function () {
        return {
          company: null,
          title: null,
          dates: null,
          description: null
        }
      }
    },
  },
  methods: {
    submit: function () {
      this.handleSubmit(this.experience);
    },
    checkForm: function () {
      const { company, title, dates, description } = this.experience;
      if (!company) {
        this.errors['company'] = "company is required";
      } else {
        delete this.errors.company;
      }

      if (!title) {
        this.errors['title'] = "title is required";
      } else {
        delete this.errors['title'];
      }

      if (!dates) {
        this.errors['dates'] = "dates is required";
      } else {
        delete this.errors['dates'];
      }

      if (!description) {
        this.errors['description'] = "description is required";
      } else {
        delete this.errors['description'];
      }

      if (this.errors['company'] || this.errors['title'] || this.errors['dates'] || this.errors['description']) {
        this.error = true;
      } else {
        this.error = false;
        this.submit();
      }

    }
  }
};
</script>
