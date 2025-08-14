<script setup lang="ts">
import { ref, provide, Transition, Teleport } from 'vue';
import AppHeader from './components/AppHeader.vue';
import ProductDetails from './components/ProductDetails.vue';
import ProductImages from './components/ProductImages.vue';
import LightboxModal from './components/LightboxModal.vue';

export type Item = {
  name: string;
  price: number;
  count: number;
  thumbnail: string;
};

const product = {
  name: 'Fall Limited Edition Sneakers',
  brand: 'Sneaker Company',
  description:
    'These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they’ll withstand everything the weather can offer.',
  price: 250,
  discount: 50,
  images: [
    'image-product-1.jpg',
    'image-product-2.jpg',
    'image-product-3.jpg',
    'image-product-4.jpg',
  ],
  thumbnails: [
    'image-product-1-thumbnail.jpg',
    'image-product-2-thumbnail.jpg',
    'image-product-3-thumbnail.jpg',
    'image-product-4-thumbnail.jpg',
  ],
};

const lightboxOpen = ref<boolean>(false);
const cartItems = ref<Item[]>([]);

function openLightbox() {
  lightboxOpen.value = true;
}

function closeLightbox() {
  lightboxOpen.value = false;
}

function addToCart(newItem: Item) {
  if (cartItems.value.some((item) => item.name === newItem.name)) {
    const targetItem = cartItems.value.find(
      (item) => item.name === newItem.name
    );
    targetItem!.count = targetItem!.count + newItem.count;
  } else {
    cartItems.value.push(newItem);
  }
}

function removeCartItem(name: string) {
  cartItems.value = cartItems.value.filter((item) => item.name != name);
}

provide('removeCartItem', removeCartItem);
</script>

<template>
  <AppHeader :cartItems="cartItems" />
  <main>
    <div class="container main-wrapper">
      <ProductImages
        @open-modal="openLightbox"
        :images="product.images"
        :thumbnails="product.thumbnails"
      />
      <ProductDetails @add-to-cart="addToCart" :product="product" />
    </div>
  </main>
  <Teleport to="body">
    <Transition>
      <LightboxModal
        v-if="lightboxOpen"
        :images="product.images"
        :thumbnails="product.thumbnails"
        @close-modal="closeLightbox"
      />
    </Transition>
  </Teleport>
</template>

<style scoped>
.main-wrapper {
  padding: 5.5rem 3rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease-in-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

@media screen and (max-width: 60rem) {
  .main-wrapper {
    padding: 3rem 1rem;
    gap: 3rem;
  }
}

@media screen and (max-width: 48rem) {
  .main-wrapper {
    grid-template-columns: 1fr;
    padding: 0;
    gap: 0;
  }
}
</style>
