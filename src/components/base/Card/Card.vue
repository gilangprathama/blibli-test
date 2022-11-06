<template>
  <div :style="`background-color: ${cardColor}; border-radius: ${borderRadius}px`" :class="cardClasses">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    cardColor: {
      type: String,
      default: '#ffffff'
    },
    borderRadius: {
      type: Number,
      default: 0,
    },
    isOutline: {
      type: Boolean,
      default: false,
    },
    isRaised: {
      type: Boolean,
      default: false,
    },
    hasShadow: {
      type: Boolean,
      default: false,
    }
  },

  computed: {
    cardClasses() {
      const cardClassesArray = ['card'];
      if (this.isOutline) {
        cardClassesArray.push('card--outlined')
      }
      if (this.isRaised) {
        cardClassesArray.push('card--raised')
      }
      if (this.hasShadow) {
        cardClassesArray.push('card--shadow')
      }
      return cardClassesArray
    }
  },
}
</script>

<style src="./Card.style.scss" lang="scss">
</style>
