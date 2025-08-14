<script setup lang="ts">
import CartItem from './CartItem.vue';

const { cartItems } = defineProps({
  cartItems: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="cart-wrapper">
    <div class="cart-header">
      <h3>Cart</h3>
    </div>
    <div v-if="cartItems.length === 0" class="cart-placeholder">
      <p>Your cart is empty.</p>
    </div>
    <div v-else class="cart-details-wrapper">
      <CartItem v-for="item in cartItems" :item="item" />
      <button class="button-checkout">Checkout</button>
    </div>
  </div>
</template>

<style scoped>
.cart-wrapper {
  position: absolute;
  z-index: 99;
  top: 100%;
  right: 0;
  width: 360px;
  border-radius: 1rem;
  box-shadow: 0 5px 15px 0 hsla(0, 0%, 0%, 0.15);
  background-color: white;
  margin-right: 1rem;
}

.cart-header {
  font-size: var(--fs-body);
  font-weight: var(--fw-bold);
  padding: 1.5rem;
  border-bottom: 1px solid var(--clr-grey-100);
}

.cart-details-wrapper {
  padding: 1.5rem;
}

.button-checkout {
  background-color: var(--clr-orange-500);
  width: 100%;
  height: 3.5rem;
  padding-inline: 4.5rem;
  border-radius: 0.5rem;
  color: white;
  border: none;
  font-weight: var(--fw-bold);
  transition: all 0.3s ease-in-out;
}

.button-checkout:hover {
  opacity: 0.7;
}

.cart-placeholder {
  width: 100%;
  height: 100px;
  display: grid;
  place-items: center;
  font-weight: var(--fw-bold);
  color: var(--clr-grey-500);
}

@media screen and (max-width: 48rem) {
  .cart-wrapper {
    width: 300px;
  }
}
</style>
