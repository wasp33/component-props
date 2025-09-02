<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <div class="col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <ProductList 
        :products="products"
        @add-cart="addCart"
        />
      </div>
      <!-- 購物車區 -->
      <Cart :carts="carts" @remove-cart="removeCart"/>
    </div>

    <!-- 通知元件 -->
    <Notification />
  </div>
</template>

<script setup>
import Cart from './components/Cart.vue';
import Notification from './components/Notification.vue';
import ProductList from './components/ProductList.vue'
import { ref, provide,reactive } from 'vue';
const products = ref([
  {
    id: 1,
    title: '耳罩式藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 2490,
    image: 'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&w=2065&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA=='
  },
  {
    id: 2,
    title: '時尚藍牙耳機',
    description: '輕巧便攜，音質出眾',
    price: 7990,
    image: 'https://images.unsplash.com/photo-1628329567705-f8f7150c3cff?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 3,
    title: '運動型藍牙耳機',
    description: '防水設計，適合運動使用',
    price: 1990,
    image: 'https://images.unsplash.com/photo-1556816692-6d32ab39b71f?q=80&w=765&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  }
]);

const carts = ref([

]);
const removeCart = (cart) => {
  // const index = carts.value.findIndex(item => item.id === cart.id);
  // if (index !== -1) {
  //   carts.value.splice(index, 1);
  // }
  carts.value = carts.value.filter(item => item.id !== cart.id);
};
const addCart = (product) => {
  const existingCartItem = carts.value.find(item => item.id === product.id);
  if (existingCartItem) {
    existingCartItem.quantity += 1;
  } else {
    carts.value.push({
      ...product,
      quantity: 1
    });
  }
};
const notificationState = reactive({
  isShow: false,
  message: ''
});
const showNotification = (message) => {
  console.log('showNotification', message);
  notificationState.message = message;
  notificationState.isShow = true;
  setTimeout(() => {
    notificationState.isShow = false;
  }, 2000);
};
provide('notificationState', notificationState);
provide('showNotification', showNotification);
</script>

<style scoped></style>
