<template>
  <div>
    <nav-bar />
    <div class="container m-container">
      <div class="p-24 flex direction-column" style="width: 100%">
        <div class="first-section pb-24">
          <card card-color="#d9fc14" class="card-container" is-outline>
            <div class="p-12">
              <p class="txt-32 txt-weight-600">1</p>
            </div>
          </card>
          <card card-color="#26f3fe" class="card-container" :border-radius="8">
            <div class="p-12">
              <p class="txt-32 txt-weight-600">2</p>
            </div>
          </card>
        </div>

        <div class="second-section pb-24">
          <card card-color="#f474ff" class="card-container">
            <div class="p-12">
              <p class="txt-32 txt-weight-600">3</p>
            </div>
          </card>
        </div>

        <div class="third-section pb-24">
          <card card-color="#ff8a8a" class="card-container">
            <div class="p-12">
              <p class="txt-32 txt-weight-600">4</p>
            </div>
          </card>
        </div>

        <div class="carousel-section pb-24">
          <carousel
            :gutter="gutter"
            :item-per-slide="itemPerSlide"
            :slide-distance="1"
          >
            <carousel-slide
              v-for="product in products"
              :key="product.id"
            >
              <product-card
                :product-img-src="product.img"
                :product-name="product.name"
                :final-price="product.finalPrice"
                :original-price="product.originalPrice"
                :is-disabled="product.isDisabled"
                :is-small="product.isSmall"
                @click-product="handleProductClick(product.id)"
                @click-to-cart="handleClickToCart(product.id)"
                class="product-card-item"
              />
            </carousel-slide>
          </carousel>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from '../components/base/Card';
import Carousel from '../components/base/Carousel/Carousel.vue';
import CarouselSlide from '../components/base/CarouselSlide/CarouselSlide.vue';
import NavBar from '../components/base/NavBar';
import ProductCard from '../components/base/ProductCard/ProductCard.vue';

export default {
  name: 'Homepage',
  components: { NavBar, Card, ProductCard, Carousel, CarouselSlide },

  data() {
    return {
      gutter: 16,
      itemPerSlide: 5,
      products: [
        {
          id: 1,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//101/MTA-11958284/nike_nike_air_jordan_1_university_blue_full03_oqkkbxoc.jpg',
          name: 'Nike Air Jordan Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1000000,
          originalPrice: 2000000,
        },
        {
          id: 2,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//92/MTA-30335527/nike_nike_dunk_low_emb_x_nba_75th_anniversary_-_chicago_bulls_full04_q4a4azwl.jpg',
          name: 'Nike Dunk Low Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
        {
          id: 3,
          img: 'https://assets.adidas.com/images/w_600,f_auto,q_auto/43c6839b25104237accbadf6009aea15_9366/RESPONSE_SHOES_Black_GW6646_41_detail.jpg',
          name: 'Adidas',
          finalPrice: 500000,
          isDisabled: true,
        },
        {
          id: 4,
          img: 'https://cf.shopee.co.id/file/e16430d95dd7df501e908a648831626e',
          name: 'Vans Oldskool',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
        {
          id: 5,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//92/MTA-30335527/nike_nike_dunk_low_emb_x_nba_75th_anniversary_-_chicago_bulls_full04_q4a4azwl.jpg',
          name: 'Nike Dunk Low Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
        {
          id: 6,
          img: 'https://assets.adidas.com/images/w_600,f_auto,q_auto/43c6839b25104237accbadf6009aea15_9366/RESPONSE_SHOES_Black_GW6646_41_detail.jpg',
          name: 'Adidas',
          finalPrice: 500000,
          isDisabled: true,
        },
        {
          id: 7,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//92/MTA-30335527/nike_nike_dunk_low_emb_x_nba_75th_anniversary_-_chicago_bulls_full04_q4a4azwl.jpg',
          name: 'Nike Dunk Low Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
        {
          id: 8,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//92/MTA-30335527/nike_nike_dunk_low_emb_x_nba_75th_anniversary_-_chicago_bulls_full04_q4a4azwl.jpg',
          name: 'Nike Dunk Low Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
        {
          id: 9,
          img: 'https://assets.adidas.com/images/w_600,f_auto,q_auto/43c6839b25104237accbadf6009aea15_9366/RESPONSE_SHOES_Black_GW6646_41_detail.jpg',
          name: 'Adidas',
          finalPrice: 500000,
          isDisabled: true,
        },
        {
          id: 10,
          img: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//92/MTA-30335527/nike_nike_dunk_low_emb_x_nba_75th_anniversary_-_chicago_bulls_full04_q4a4azwl.jpg',
          name: 'Nike Dunk Low Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua',
          finalPrice: 1500000,
          originalPrice: 2000000,
        },
      ]
    };
  },

  methods: {
    handleProductClick(productId) {
      alert(`Product ID ${productId} clicked!`)
    },
    handleClickToCart(productId) {
      alert(`Product ID ${productId} successfully added to your cart!`)
    }
  },
}
</script>

<style lang="scss" scoped>
.first-section,
.second-section,
.third-section {
  display: grid;
  grid-column-gap: 24px;
}

.first-section {
  @media (max-width: 989px) {
    order: 4;
  }
}

.second-section {
  @media (max-width: 989px) {
    order: 2;
  }
}

.third-section {
  @media (max-width: 989px) {
    order: 1;
  }
}

.carousel-section {
  @media (max-width: 989px) {
    order: 3;
  }
}

.card-container {
  grid-row: 1;
  width: 100%;
  height: 200px;
  align-items: center;
  justify-content: center;
}

.product-card-item {
  float: left;
  margin-right: 18px;

  &:last-child {
    margin-right: 0;
  }
}
</style>
