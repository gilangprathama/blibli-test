<template>
  <div
    ref="parentSlide"
    class="carousel"
  >
    <div
      class="carousel__wrapper"
    >
      <div
        ref="carouselSlide"
        class="carousel__container"
        :style="carouselSlideStyle"
      >
        <slot></slot>
      </div>
    </div>

    <div
      v-if="carouselActive()"
      class="carousel__navigation"
    >
      <button
        class="carousel__navigation-prev"
        @click.stop="throttledClick(activeSlideIndex - 1)"
        :disabled="handleDisabledNavigator('prev')"
        style="left: -24px"
      >
        &lsaquo;
      </button>
      <button
        class="carousel__navigation-next"
        @click.stop="throttledClick(activeSlideIndex + 1)"
        :disabled="handleDisabledNavigator('next')"
        style="right: -24px"
      >
        &rsaquo;
      </button>
    </div>
  </div>
</template>

<script>
import throttle from './throttle';

export default {
  name: 'Carousel',
  props: {
    itemPerSlide: {
      type: Number,
      default: 1,
    },
    gutter: {
      type: Number,
      default: 0,
    },
    slideDistance: {
      type: Number,
      default: 1,
    },
  },

  data() {
    return {
      carouselSlide: null,
      totalSlide: null,
      activeSlideIndex: 0,
      bannerWidth: 800,
    };
  },

  computed: {
    activeSlidePosition() {
      return this.handleSlidePosition()
    },
    carouselSlideStyle() {
      return `
          margin-left: ${this.gutter ? `-${this.gutter / 2}px` : ''};
          margin-right: ${this.gutter ? `-${this.gutter / 2}px` : ''};
          transform: translateX(${this.activeSlidePosition});
        `
    },
  },

  created() {
    this.throttledClick = throttle(400, true, index => {
      if (index === this.activeSlideIndex + 1) {
        this.nextSlide()
      } else if (index === this.activeSlideIndex - 1) {
        this.prevSlide()
      }
    })
  },

  mounted() {
    this.handleInitCarousel();

    this.$nextTick(() => {
      this.setBannerWidth();
      window.addEventListener('resize', () => {
        this.setBannerWidth();
      });
    })
  },

  methods: {
    setBannerWidth() {
      this.bannerWidth =
        (this.$refs.carouselSlide &&
          this.$refs.carouselSlide.children[0] &&
          this.$refs.carouselSlide.children[0].clientWidth) ||
        0;
    },
    carouselActive() {
      return this.totalSlide > this.itemPerSlide
    },
    handleInitCarousel() {
      this.carouselSlide = this.$refs.carouselSlide;
      this.totalSlide = this.carouselSlide ? this.carouselSlide.children.length : 0;
    },
    nextSlide() {
      const nextSlidesEnough =
        this.totalSlide - (this.itemPerSlide + this.activeSlideIndex) >=
        this.slideDistance

      if (nextSlidesEnough) {
        this.activeSlideIndex += this.slideDistance
      } else {
        this.activeSlideIndex++
      }

      this.$emit('nextSlide', this.activeSlideIndex)
      this.carouselSlide.classList.add('is-animation')
    },
    prevSlide() {
      const prevSlidesEnough = this.activeSlideIndex >= this.slideDistance

      if (prevSlidesEnough) {
        this.activeSlideIndex -= this.slideDistance
      } else {
        this.activeSlideIndex--
      }

      this.$emit('prevSlide', this.activeSlideIndex)
      this.carouselSlide.classList.add('is-animation')
    },
    lastSlide() {
      return this.activeSlideIndex === this.totalSlide - this.itemPerSlide
    },
    handleDisabledNavigator(value) {
      if (this.carouselActive()) {
        if (value === 'next') {
          return this.lastSlide()
        }
        if (value === 'prev') {
          return this.activeSlideIndex === 0
        }
      }
      return true
    },
    handleSlidePosition() {
      let bannerWidth = this.bannerWidth
      let setPosition = this.activeSlideIndex * bannerWidth

      if (this.lastSlide()) {
        setPosition -= this.gutter - 2
      }
      return `-${setPosition}px`
    },
  },
}
</script>

<style src="./Carousel.style.scss" lang="scss">
</style>
