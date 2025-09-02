<template>
      <div class="col-md-4">
      <h2 class="mb-3">購物車</h2>
      <div v-if="carts.length === 0">購物車是空的</div>
      <ul class="list-group mb-3">
        <li v-for="cart in carts" class="list-group-item d-flex justify-content-between align-items-center">
          <div>
            <h6 class="my-0">{{ cart.title }}</h6>
            <small class="text-muted">數量：{{ cart.quantity }}</small>
          </div>
          <div>
            <span class="text-muted">${{ cart.price }}</span>
            <button class="btn btn-sm btn-outline-danger ms-2" @click="removeFromCart(cart)"> 移除 </button>
          </div>
        </li>
      </ul>
    </div>
</template>
<script setup>
import { inject } from 'vue';
const props = defineProps({
  carts: {
    type: Array,
    required: true
  }
});
const emit = defineEmits(['remove-cart']);
const removeFromCart = (cart) => {
  emit('remove-cart', cart);
  showNotification(`已將 ${cart.title} 從購物車移除`)
};

const showNotification = inject('showNotification');

</script>
