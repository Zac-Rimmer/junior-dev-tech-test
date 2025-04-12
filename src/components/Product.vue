<template>
  <div id="product" class="product-container">
    <div class="row justify-content-center">
      <div class="col-md-12 col-lg-7">
        <div class="row g-3 mb-5">
          <div
            class="col-sm-12 col-md-6"
            v-for="(image, index) in product.media_gallery"
            :key="index"
          >
            <img :src="image.image" :alt="image.alt" class="img-fluid" />
          </div>
        </div>
      </div>
      <div class="col-md-12 col-lg-4">
        <p class="offer-text small">{{ product.product_offer_label }}</p>
        <h6 class="title poppins-semibold">
          {{ `${product.product_title} | ${product.product_colour}` }}
        </h6>
        <hr class="h-line" />
        <div class="d-flex justify-content-between small">
          <div class="d-flex gap-3">
            <div>
              Original<br />
              <span :class="{ 'text-decoration-line-through': isDiscounted }">
                {{ `£${product.rrp}` }}.00
              </span>
            </div>
            <div v-show="isDiscounted">
              Now<br />
              <span class="text-danger">
                {{ `£${product.selling_price}` }}.00
              </span>
            </div>
          </div>
          <span
            v-show="isDiscounted"
            class="text-danger align-self-center discount"
          >
            {{ isDiscounted ? `Save ${discountPercentage}%` : "" }}
          </span>
        </div>
        <hr class="h-line" />
        <div class="row g-3">
          <div
            v-for="(colour, index) in product.alternative_colours"
            :key="index"
            class="col-auto"
          >
            <a :href="colour.url" :title="colour.alt_text">
              <img
                :src="colour.image"
                :alt="colour.alt_text"
                :width="65"
                class="img-fluid"
              />
            </a>
          </div>
        </div>
        <hr class="h-line" />
        <div class="my-4">
          <label class="text-muted small mb-1" for="size-select">Size</label>
          <div class="d-flex gap-2" style="flex-wrap: nowrap">
            <button
              v-for="size in product.product_size_labels"
              :key="size"
              class="size-btn btn"
              :class="{
                'btn-outline-secondary': selectedSize !== size,
                'btn-secondary active': selectedSize === size,
              }"
              @click="selectSize(size)"
            >
              <div class="small">{{ size }}</div>
            </button>
          </div>
        </div>
        <hr class="h-line" />
        <button
          type="button"
          @click="addItemToBag"
          class="add-btn btn bg-black text-white rounded-pill w-100"
        >
          Add To Bag
        </button>
        <h6 class="mt-3 mb-2 poppins-regular">Description</h6>
        <p class="small poppins-light">{{ product.product_description }}</p>
        <p
          v-html="product.product_bulletpoints"
          class="small poppins-medium"
        ></p>
        <p>
          <span class="small poppins-medium">Product Code: </span>
          <span class="text-muted">{{ product.product_sku }}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import product from "./data/product.json";

export default {
  name: "ProductPage",
  data() {
    return {
      product: product,
      selectedSize: null,
    };
  },
  computed: {
    isDiscounted() {
      return this.product.rrp > this.product.selling_price;
    },
    discountPercentage() {
      return this.isDiscounted
        ? ((this.product.rrp - this.product.selling_price) / this.product.rrp) *
            100
        : 0;
    },
  },
  methods: {
    selectSize(size) {
      this.selectedSize = size;
    },
    addItemToBag() {
      alert(
        this.selectedSize
          ? `You have selected size: ${this.selectedSize}`
          : "Please select a size."
      );
    },
  },
};
</script>

<style scoped lang="scss">
.offer-text {
  border-left: 5px peach;
  padding-left: 5px;
}

.h-line {
  background-color: grey;
  height: 1px;
  border: none;
}

.size-btn {
  height: 50px;
  width: 65px;
  transition: background-color 0.3s ease;
}

.size-btn:hover {
  background-color: black;
  color: white;
}

.size-btn.active {
  background-color: black;
  color: white;
}

.add-btn {
  padding: 0.7rem 0;
}

.discount {
  border-left: 2px solid red;
  border-right: 2px solid red;
  padding: 0 1rem;
}

@media (min-width: 1200px) {
  .container {
    max-width: 1500px;
  }
}
</style>
