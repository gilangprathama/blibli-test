<template>
  <card :class="productCardClasses" card-color="#ffffff" :border-radius="12" has-shadow>
    <figure>
      <a @click="handleClickProduct"><img :src="productImgSrc" :alt="productName"></a>
      <figcaption>
        <div class="product-card__content">
          <a @click="handleClickProduct"><div class="product-card__title">
            {{ productName }}
          </div></a>
          <div class="product-card__price">
            <p class="product-card__price--final">{{ money(finalPrice) }}</p>
            <div class="product-card__price--disount" v-if="originalPrice != 0">
              <span class="price-original">{{ money(originalPrice) }}</span>
              <span class="price-discount-percentage">{{ percentage }}</span>
            </div>
          </div>
        </div>
        <bli-button @click="handleClickToCart" :is-disabled="isDisabled">
          {{ actionButtonText }}
        </bli-button>
      </figcaption>
    </figure>
  </card>
</template>

<script>
import Card from '../Card';
import BliButton from '../BliButton';

export default {
  name: 'ProductCard',
  components: { Card, BliButton },

  props: {
    productImgSrc: {
      type: String,
      default: '',
    },
    productName: {
      type: String,
      default: '',
      required: true,
    },
    finalPrice: {
      type: Number,
      default: 0,
      required: true,
    },
    originalPrice: {
      type: Number,
      default: 0,
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    isSmall: {
      type: Boolean,
      dafault: false,
    }
  },

  computed: {
    productCardClasses() {
      const productCardClassesArray = ['product-card'];

      if (this.isSmall) {
        productCardClassesArray.push('is-small');
      }

      return productCardClassesArray;
    },
    percentage() {
      if (this.originalPrice !== 0) {
        return `${(100 * (this.originalPrice - this.finalPrice) / this.originalPrice).toFixed(0)}%`;
      }
      return;
    },
    actionButtonText() {
      return this.isDisabled ? 'Out of stock' : 'Add to bag';
    }
  },

  methods: {
    money(price) {
      return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(price);
    },
    handleClickProduct() {
      this.$emit('click-product');
    },
    handleClickToCart() {
      this.$emit('click-to-cart');
    }
  },
}
</script>

<style src="./ProductCard.style.scss" lang="scss">
</style>