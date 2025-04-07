<template>
  <div id="product">
    <!-- Add your code here -->
    <p>{{ product.product_offer_label }}</p>
    <h1 class="text-center">{{ product.product_title }}</h1>
    <p>Original</p>
    <p class="text-decoration-line-through">£{{ product.rrp }}.00</p>
    <p>Now</p>
    <p>£{{ product.selling_price }}.00</p>
    <p>Select Size</p>
    <ul class="list-unstyled">
      <li v-for="size in sizes">{{ size }}</li>
    </ul>
    <button>Add To Bag</button>
    <h2>Description</h2>
    <p>{{ product.product_description }}</p>
    <div v-html="bulletpoints"></div>
    <p>Product Code: {{ product.product_sku }}</p>

    <img
      v-for="media in mediaGallery"
      :src="media.image"
      :width="media.width"
      :height="media.height"
    />
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
// Styling to be added here if needed. SASS is allowed if preferred
</style>
