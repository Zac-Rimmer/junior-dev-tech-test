<template>
  <div id="product" class="container">
    <div class="row">
      <div class="col-md-12 col-lg-8">
        <div class="row g-3 mb-4">
          <div class="col-sm-12 col-md-6" v-for="(image, index) in product.media_gallery" :key="index">
            <img :src="image.image" :alt="image.alt" class="img-fluid">
          </div>
        </div>
      </div>
      <div class=" col-md-12 col-lg-4">
        <p class="offer-text small">{{ product.product_offer_label }}</p>
        <h6 class="poppins-semibold">{{ product.product_title + " | " + product.product_colour }}</h6>
        <hr class="h-line">
        <div class="d-flex justify-content-between small ">
          <div class="d-flex gap-3">
            <span>Original<br>£{{ product.rrp.toFixed(2) }}</span>
            <div>Now<br> <span class="text-danger">£{{ product.selling_price.toFixed(2) }}</span> </div>
          </div>
          <span class="text-danger align-self-center">| Save {{ }} |</span>
        </div>
        <hr class="h-line">
        <div class="row g-3">
          <div v-for="(colour, index) in product.alternative_colours" :key="index" class="col-auto">
            <a :href="colour.url" :title="colour.alt_text" style="display: inline-block;">
              <img :src="colour.image" :alt="colour.alt_text" :width="60" :height="60" class="img-fluid">
            </a>
          </div>
        </div>
        <hr class="h-line">
        <div class="my-4">
          <label class="text-muted small mb-1" for="size-select">Select Size</label>
          <div class="d-flex flex-wrap gap-2">
            <button v-for="size in product.product_size_labels" :key="size"
              class="size-button btn btn-outline-secondary rounded-0 flex-fill" @click="selectedSize = size">
              <div class="small">{{ size }}</div>
            </button>
          </div>
        </div>
        <hr class="h-line">
        <button type="button" class="add-to-cart-btn btn bg-black text-white rounded-pill w-100">Add To Bag</button>
        <p class="mt-3 mb-2">Description</p>
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
  // Any Vue lifecycle hooks and custom JavaScript code can be added here
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
  height: 45px;
}

.add-to-cart-btn {
  padding-top: 0.55rem;
  padding-bottom: 0.55rem;
}

#product.container {
  // did not want to mess around container-fluid
  max-width: 1550px;
}
</style>
