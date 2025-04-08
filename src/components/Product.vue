<template>
  <div id="product">
    <!-- Add your code here -->
    <div class="container font-adjust">
      <div class="row">
        <div id="image-gallery" class="col">
          <img
            v-for="media in mediaGallery"
            :height="media.height"
            :width="media.width"
            :src="media.image"
            :alt="media.alt"
            :class="media.alt"
          />
        </div>
        <div class="col-4 p-0">
          <p class="offer">
            {{ product.product_offer_label }}
          </p>
          <h1 class="text-left font-weight-bold border-bottom">
            {{ product.product_title }} | {{ product.product_colour }}
          </h1>
          <div id="pricing" class="d-flex border-bottom pb-1">
            <div>
              <p class="m-1">Original</p>
              <p class="text-decoration-line-through m-1">
                £{{ product.rrp }}.00
              </p>
            </div>
            <div>
              <p class="my-1 mx-2">Now</p>
              <p class="my-1 mx-2 selling-price">
                £{{ product.selling_price }}.00
              </p>
            </div>
            <p class="selling-price ms-auto align-self-center my-0">
              | Save 35% |
            </p>
          </div>
          <div class="colour-images border-bottom py-2">
            <img
              v-for="colour in altColours"
              :width="70"
              :height="70"
              :src="colour.image"
              :alt="colour.alt"
            />
          </div>
          <div class="border-bottom py-3">
            <p class="mb-0 pt-2 pb-1 poppins-light">Select Size</p>
            <div class="w-100 d-flex flex-wrap sizes">
              <button
                v-for="size in sizes"
                class="font-adjust size-group-item poppins-light btn btn-outline-dark"
              >
                {{ size }}
              </button>
            </div>
          </div>
          <button
            class="font-adjust rounded-pill w-100 btn btn-dark p-2 mx-1 my-2"
          >
            Add To Bag
          </button>
          <section id="description" class="py-1">
            <h3>Description</h3>
            <p class="poppins-light">{{ product.product_description }}</p>
            <div v-html="bulletpoints"></div>
            <p>
              Product Code:<span class="poppins-light">
                {{ product.product_sku }}</span
              >
            </p>
          </section>
        </div>
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
      sizes: product.product_size_labels,
      bulletpoints: product.product_bulletpoints,
      mediaGallery: product.media_gallery,
      altColours: product.alternative_colours,
    };
  },
  // Any Vue lifecycle hooks and custom JavaScript code can be added here
};
</script>

<style scoped lang="scss">
#image-gallery {
  margin-bottom: 1rem;
}
#image-gallery > * {
  width: 49%;
  height: auto;
  padding-inline: 0.7rem;
  padding-bottom: 1.4rem;
}
.font-adjust {
  font-size: 12px;
}
h1 {
  font-size: 15px;
}
h3 {
  font-size: 14px;
}
.colour-images > * {
  padding: 0.5em;
}
.selling-price {
  color: #b32a2d;
}
.offer {
  padding-left: 0.3em;
  margin-top: 0.5em;
  border-left-width: 0.3em !important;
  border-left: solid;
  border-left-color: #bb5400;
}
.size-group-item {
  width: 12.9%;
  padding-top: 5%;
  padding-bottom: 5%;
  padding-inline: 0;
  line-height: 0;
  margin-right: 0.5em;
  border-radius: 0 !important;
  border-color: black;
}
// Styling to be added here if needed. SASS is allowed if preferred
</style>
