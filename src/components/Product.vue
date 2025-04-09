<template>
  <div id="product" class="container">
    <div class="row justify-content-center">
      <div class="col-md-12 col-lg-7 ">
        <div class="row g-3 mb-5 ">
          <div class="col-sm-12 col-md-6 " v-for="(image, index) in product.media_gallery" :key="index">
            <img :src="image.image" :alt="image.alt" class="img-fluid m-0 p-0">
          </div>
        </div>
      </div>
      <div class=" col-md-12 col-lg-4">
        <p class="offer-text small">{{ product.product_offer_label }}</p>
        <h6 class="poppins-semibold">{{ product.product_title + " | " + product.product_colour }}</h6>
        <hr class="h-line">
        <div class="d-flex justify-content-between small ">
          <div class="d-flex gap-3">
            <span>Original<br><span :class="{ 'text-decoration-line-through': hasDiscount }">£{{ product.rrp.toFixed(2)
                }}</span></span>
            <div v-if="hasDiscount">Now<br> <span class="text-danger">£{{ product.selling_price.toFixed(2) }}</span>
            </div>
          </div>
          <span v-if="hasDiscount" class="text-danger align-self-center discount">Save {{ discount }} %</span>
        </div>
        <hr class="h-line">
        <div class="row g-3">
          <div v-for="(colour, index) in product.alternative_colours" :key="index" class="col-auto">
            <a :href="colour.url" :title="colour.alt_text">
              <img :src="colour.image" :alt="colour.alt_text" :width="65" class="img-fluid">
            </a>
          </div>
        </div>
        <hr class="h-line">
        <div class="my-4">
          <label class="text-muted small mb-1" for="size-select">Select Size</label>
          <div class="d-flex flex-wrap gap-2">
            <button v-for="size in product.product_size_labels" :key="size" class="size-button btn rounded-0" :class="{
              'btn-outline-secondary': selectedSize !== size,
              'btn-secondary active': selectedSize === size
            }" @click="selectedSize = size">
              <div class="small">{{ size }}</div>
            </button>
          </div>
        </div>
        <hr class="h-line">
        <button type="button" :disabled="!selectedSize" @click="addToBag"
          class="add-to-cart-btn btn bg-black text-white rounded-pill w-100">Add To Bag</button>
        <h6 class="mt-3 mb-2 poppins-regular">Description</h6>
        <p class="small poppins-light">{{ product.product_description }}</p>
        <p v-html="product.product_bulletpoints" class="small poppins-medium "></p>
        <p>
          <span class="small poppins-medium">Product Code: </span>
          <span class="text-muted">{{ product.product_sku }}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import product from './data/product.json'

export default {
  name: 'ProductPage',
  data() {
    return {
      product: product,
      selectedSize: null,
    }
  },
  computed: {
    hasDiscount() {
      return this.product.rrp > this.product.selling_price;
    },
    discount() {
      if (this.hasDiscount) {
        const discount = this.product.rrp - this.product.selling_price;
        return Math.round((discount / this.product.rrp) * 100);
      }
      return 0;
    }
  },
  methods: {
    addToBag() {
      if (this.selectedSize) {
        alert(`Your selected size: ${this.selectedSize}`);
      }
    }
  }
}
</script>

<style scoped lang="scss">
.offer-text {
  border-left: 5px solid rgb(205, 96, 19);
  padding-left: 5px;
}

.h-line {
  background-color: rgb(168, 166, 166);
  height: 1px;
  border: none;
}

.size-button {
  height: 50px;
  width: 65px;
}

.add-to-cart-btn {
  padding: 0.7rem 0;
}

.discount {
  border-left: 2px solid red;
  border-right: 2px solid red;
  padding-left: 0.5em;
  padding-right: 0.5em;
}

.btn-outline-secondary.active {
  background-color: #007bff;
  color: white;
  border-color: #007bff;
}

@media (min-width: 1320px) {

  // when the screen is more than xxl, we make the standart container bigger
  .container {
    max-width: 1600px;
  }
}
</style>
