<script setup lang="ts">
import { ref } from 'vue';

const itemCount = ref<number>(0);

function addItemCount() {
  itemCount.value = itemCount.value + 1;
}

function removeItemCount() {
  if (itemCount.value === 0) return;

  itemCount.value = itemCount.value - 1;
}

const emit = defineEmits(['addToCart']);

function handleAddToCart() {
  emit('addToCart', itemCount.value);
}
</script>

<template>
  <div class="cart-actions-wrapper">
    <div class="cart-count-wrapper">
      <button class="cart-count-btn" @click="removeItemCount">
        <span class="sr-only">remove product count</span>
        <svg
          class="icon-minus"
          width="12"
          height="4"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
        >
          <defs>
            <path
              d="M11.357 3.332A.641.641 0 0 0 12 2.69V.643A.641.641 0 0 0 11.357 0H.643A.641.641 0 0 0 0 .643v2.046c0 .357.287.643.643.643h10.714Z"
              id="a"
            />
          </defs>
          <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#a" />
        </svg>
      </button>
      <span class="product-count">{{ itemCount }}</span>
      <button class="cart-count-btn" @click="addItemCount">
        <span class="sr-only">add product count</span>
        <svg
          class="icon-plus"
          width="12"
          height="12"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
        >
          <defs>
            <path
              d="M12 7.023V4.977a.641.641 0 0 0-.643-.643h-3.69V.643A.641.641 0 0 0 7.022 0H4.977a.641.641 0 0 0-.643.643v3.69H.643A.641.641 0 0 0 0 4.978v2.046c0 .356.287.643.643.643h3.69v3.691c0 .356.288.643.644.643h2.046a.641.641 0 0 0 .643-.643v-3.69h3.691A.641.641 0 0 0 12 7.022Z"
              id="b"
            />
          </defs>
          <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#b" />
        </svg>
      </button>
    </div>
    <button @click="handleAddToCart" class="add-to-cart-btn">
      <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
          fill="#FFFFFF"
          fill-rule="nonzero"
        />
      </svg>
      <span>Add to cart</span>
    </button>
  </div>
</template>

<style scoped>
.cart-actions-wrapper {
  display: flex;
  gap: 1rem;
}

.cart-count-wrapper {
  background-color: var(--clr-grey-100);
  height: 3.5rem;
  padding-inline: 1rem;
  border-radius: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 3rem;
}

.cart-count-btn {
  background-color: transparent;
  border: none;
  transform: all 0.3s ease-in-out;
}

.cart-count-btn:hover,
.add-to-cart-btn:hover {
  opacity: 0.7;
}

.product-count {
  font-weight: var(--fw-bold);
}

.add-to-cart-btn {
  background-color: var(--clr-orange-500);
  height: 3.5rem;
  padding-inline: 4.5rem;
  border-radius: 0.5rem;
  color: white;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  font-weight: var(--fw-bold);
  transition: all 0.3s ease-in-out;
}

.add-to-cart-btn > * {
  flex-shrink: 0;
}

@media screen and (max-width: 48rem) {
  .cart-actions-wrapper {
    flex-direction: column;
    align-items: stretch;
    justify-content: center;
    width: 100%;
  }

  .cart-count-wrapper {
    justify-content: space-between;
  }
}
</style>
