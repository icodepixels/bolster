<template>
  <button
    :class="buttonClass"
    @click="onClick"
    :title="this.buttonTitle"
    type="button"
  >{{ this.buttonTitle }}</button>
</template>

<style>
.Button {
  align-items: center;
  background-color: #81b247;
  border: 1px solid #81b247;
  border-radius: 4px;
  color: #fff;
  display: flex;
  letter-spacing: 1px;
  font-size: 1em;
  font-weight: 500;
  justify-content: center;
  padding: 12px;
  text-transform: capitalize;
}
.Button:hover {
  cursor: pointer;
  border: 1px solid #1b240e;
  transition: border 0.3s ease-in;
}
.Text {

}
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