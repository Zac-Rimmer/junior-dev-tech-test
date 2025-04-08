<template>
  <div id="product">
    <!-- Add your code here -->
    <div class="container-flex">
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
        <div class="col-4">
          <p class="offer">
            {{ product.product_offer_label }}
          </p>
          <p class="text-left font-weight-bold border-bottom h4">
            {{ product.product_title }} | {{ product.product_colour }}
          </p>
          <div id="pricing" class="d-flex border-bottom">
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
          </div>
          <div class="colour-images">
            <img
              v-for="colour in altColours"
              :width="100"
              :height="100"
              :src="colour.image"
              :alt="colour.alt"
            />
          </div>
          <p>Select Size</p>
          <ul class="list-group list-group-horizontal">
            <li v-for="size in sizes" class="list-group-item px-3">
              {{ size }}
            </li>
          </ul>
          <button class="rounded-pill w-100 border-dark bg-dark text-light">
            Add To Bag
          </button>
          <h3>Description</h3>
          <p>{{ product.product_description }}</p>
          <div v-html="bulletpoints"></div>
          <p>Product Code: {{ product.product_sku }}</p>
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

      // Add any other data properties you need
    };
  },
  // Any Vue lifecycle hooks and custom JavaScript code can be added here
};
</script>

<style scoped lang="scss">
#image-gallery {
  margin-left: 2rem;
  margin-bottom: 1rem;
}
#image-gallery > * {
  width: 50%;
  height: auto;
  padding-inline: 0.7rem;
  padding-bottom: 1.4rem;
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
.list-group-item {
  margin: 0.2em;
  border-left-width: 2px !important;
  border-radius: 0 !important;
  border-width: 2px !important;
  border-color: black;
}
// Styling to be added here if needed. SASS is allowed if preferred
</style>
