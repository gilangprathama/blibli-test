<template>
  <button @click="handleClick" :class="buttonClasses" :disabled="isDisabled">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'BliButton',
  props: {
    isDisabled: {
      type: Boolean,
      default: false,
    }
  },

  computed: {
    buttonClasses() {
      const buttonClassesArray = ['bli-button'];

      if (this.isDisabled) {
        buttonClassesArray.push('is-disabled');
      }

      return buttonClassesArray;
    }
  },

  methods: {
    handleClick() {
      this.$emit('click')
    }
  },
}
</script>

<style src="./BliButton.style.scss" lang="scss">
</style>
