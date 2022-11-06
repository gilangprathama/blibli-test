<template>
  <div
    tabindex="-1"
    class="carousel-slide"
    :style="itemSlideStyle"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'CarouselSlide',

  computed: {
    parent() {
      let parent = this.$parent;
      while (parent && parent.$options.componentName === 'Carousel') {
        parent = parent.$parent;
      }
      return parent
    },
    gutter() {
      return this.parent ? this.parent.gutter : 0;
    },
    itemPerSlide() {
      return this.parent ? this.parent.itemPerSlide : 1;
    },
    itemSlideStyle() {
      return`
        padding-left: ${this.gutter ? `${this.gutter / 2}px` : ''};
        padding-right: ${this.gutter ? `${this.gutter /2}px` : ''};
        flex: 1 0 ${this.itemPerSlide ? `${100 / this.itemPerSlide}%`: ''};
        max-width: ${this.itemPerSlide ? `${100 / this.itemPerSlide}%` : ''};
      `
    }
  },
}
</script>

<style src="./CarouselSlide.style.scss" lang="scss">
</style>
