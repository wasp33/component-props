<template>
  <div class="row">
    <div v-for="product in products" class="col-md-4 mb-4">
      <div class="card h-100">
        <img
          :src="product.image"
          class="card-img-top">
        <div class="card-body">
          <h5 class="card-title">{{ product.title}}</h5>
          <p class="card-text">{{ product.description }}</p>
          <p class="fw-bold text-primary">$ {{ product.price }}</p>
          <button class="btn btn-success w-100" @click="addToCart(product)"> 加入購物車 </button>
        </div>
      </div>
    </div>
  </div>

</template>
<script setup>
import { inject } from 'vue';
const props = defineProps({
  products: {
    type: Array,
    required: true
  }
});
const emit = defineEmits(['add-cart']);
const addToCart = (product) => {
  emit('add-cart', product);
  showNotification(`已將 ${product.title} 加入購物車`);
};
const showNotification = inject('showNotification');

</script>