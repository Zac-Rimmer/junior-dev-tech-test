<template>
  <div id="product">
    <!-- Add your code here -->
    <div class="container-fluid">
      <div class="row">
        <div id="image-gallery" class="col-sm">
          <img
            v-for="media in mediaGallery"
            :src="media.image"
            :alt="media.alt"
          />
        </div>
        <div class="col-sm">
          <p class="offer">
            {{ product.product_offer_label }}
          </p>
          <p class="text-left font-weight-bold border-bottom">
            {{ product.product_title }} | {{ product.product_colour }}
          </p>
          <img
            v-for="media in mediaGallery"
            :src="media.image"
            :alt="media.alt"
          />
          <p>Original</p>
          <p class="text-decoration-line-through">£{{ product.rrp }}.00</p>
          <p>Now</p>
          <p>£{{ product.selling_price }}.00</p>
          <p>Select Size</p>
          <ul class="list-group list-group-horizontal">
            <li v-for="size in sizes" class="list-group-item">{{ size }}</li>
          </ul>
          <button>Add To Bag</button>
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
      imgPath: product.media_gallery[0].image,

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
  padding: 0.5rem;
}
.offer {
  padding-left: 0.3em;
  border-left-width: 0.3em !important;
  border-left: solid;
  border-left-color: #bb5400;
}
.list-group-item {
  margin: 0.5em;
  border-left-width: 2px !important;
  border-radius: 0 !important;
  border-width: 2px;
  border-color: black;
}
// Styling to be added here if needed. SASS is allowed if preferred
</style>
