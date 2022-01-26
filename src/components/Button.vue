<template>
  <button
    :class="buttonClass"
    @click="onClick"
    :title="buttonTitle"
    type="button"
  >{{ buttonTitle }}</button>
</template>

<style>
  @import './Button.css';
</style>

<script>
export default {
  props: {
    buttonClass: {
      type: String
    },
    buttonTitle: {
      type: String
    },
    onClick: {
      type: Function,
      required: true
    }
  }
}
</script>