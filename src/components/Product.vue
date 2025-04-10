<template>
  <div id="product">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-6">
          <div class="row">
            <div
              v-bind:key="image.alt"
              v-for="image in product.media_gallery"
              class="col-12 col-md-6 mb-4"
            >
              <img :src="image.image" :alt="image.alt" class="img-fluid" />
            </div>
          </div>
          <hr />
        </div>

        <div class="col-12 col-md-6">
          <div class="info-container">
            <div class="offer-indent"></div>
            <p>{{ product.product_offer_label }}</p>
          </div>

          <h1>{{ product.product_title }}</h1>

          <hr />

          <div
            class="col d-flex justify-content-between align-items-center pricing-bar"
          >
            <div class="d-flex">
              <div>
                <p>Original</p>
                <p class="original_price pricing-bar-prices">
                  £{{ product.rrp }}.00
                </p>
              </div>

              <div class="text-margin">
                <p>Now</p>
                <p class="offer_text pricing-bar-prices">
                  £{{ getDiscountedPrice(product.rrp) }}
                </p>
              </div>
            </div>

            <div>
              <p class="offer_text">| Save 50% |</p>
            </div>
          </div>

          <hr />

          <section class="row">
            <div
              v-bind:key="image.alt_text"
              v-for="image in product.alternative_colours"
              class="col-auto"
            >
              <a :href="image.url" target="_blank" class="img-link">
                <img :src="image.image" :alt="image.alt_text" />
              </a>
            </div>
          </section>

          <hr />

          <p class="secondary-text">Select Size</p>
          <section class="row">
            <div
              v-bind:key="size"
              v-for="size in product.product_size_labels"
              class="col"
              @click="setSelectedSize(size)"
            >
              <button
                type="button"
                class="button-sizing secondary-text w-100"
                :class="{ active: selectedSize === size }"
              >
                {{ size }}
              </button>
            </div>
          </section>

          <hr />

          <button
            type="button"
            class="btn button-primary w-100"
            @click="addToBag(selectedSize)"
          >
            Add To Bag
          </button>

          <h2 :style="{ fontWeight: 400 }">Description</h2>
          <p class="secondary-text" :style="{ fontWeight: 300 }">
            {{ product.product_description }}
          </p>

          <div v-html="product.product_bulletpoints"></div>

          <div class="info-container">
            <p>Product Code:</p>
            <p :style="{ fontWeight: 300 }">{{ product.product_sku }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import product from ".//data/product.json";

export default {
  name: "ProductPage",
  data() {
    return {
      product: product,
      // Add any other data properties you need
      selectedSize: null,
      bag: [],
    };
  },
  // Any Vue lifecycle hooks and custom JavaScript code can be added here
  methods: {
    getDiscountedPrice(rrp) {
      return (rrp * 0.5).toFixed(2);
    },
    setSelectedSize(size) {
      this.selectedSize = size;
    },
    addToBag(selectedSize) {
      if (selectedSize === null) {
        alert(`Please select a size.`);
      } else {
        this.bag.push(selectedSize);
        alert(`You have selected size: ${selectedSize}`);
      }
    },
  },
};
</script>

<style scoped lang="scss">
// Styling to be added here if needed. SASS is allowed if preferred
* {
  color: #343334;
}
hr {
  color: #c7c7c7;
}
h1 {
  font-size: 20px;
}
h2 {
  font-size: 16px;
}
.secondary-text {
  color: #4f4f4f;
}
.original_price {
  text-decoration: line-through;
}
.pricing-bar {
  margin-bottom: -16px;
}
.pricing-bar-prices {
  margin-top: -16px;
}
.offer_text {
  color: #b3292d;
}
.offer-indent {
  background-color: #bb5401;
  height: 22px;
  width: 4px;
}
.text-margin {
  margin-left: 12px;
}
.info-container {
  display: flex;
  padding: 0px;
  gap: 4px;
}
.alt-colours-row {
  padding: 0px;
  display: flex;
}
.button-primary {
  background-color: black;
  color: white;
  border-radius: 24px;
  margin-bottom: 24px;
  padding: 12px;
}
.button-primary:hover {
  background-color: #333333;
  color: white;
}
.button-sizing {
  width: 24px;
  padding: 24px;
  background-color: white;
  border-radius: 0px;
  border: 1px solid black;
  padding: 16px;
  margin-bottom: 16px;
}
.button-sizing:hover {
  color: white;
  background-color: black;
  border: 1px solid black;
}
.img-link img {
  height: 60px;
  width: auto;
}
button.active {
  color: white;
  background-color: black;
  border: 1px solid black;
}
</style>
