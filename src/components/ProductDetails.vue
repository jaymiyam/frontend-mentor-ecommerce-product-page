<script setup lang="ts">
import CartActions from './CartActions.vue';
import type { Item } from '@/App.vue';

const { product } = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['addToCart']);

function formatPrice(price: number): string {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  }).format(price);
}

function handleAddToCart(itemCount: number) {
  const newItem: Item = {
    name: product.name,
    price: (product.price * product.discount) / 100,
    count: itemCount,
    thumbnail: product.thumbnails[0],
  };

  emit('addToCart', newItem);
}
</script>

<template>
  <div class="product-details-wrapper">
    <div>
      <h2 class="product-brand">{{ product.brand }}</h2>
      <h1 class="product-name">{{ product.name }}</h1>
    </div>
    <div>
      <p class="product-description">{{ product.description }}</p>
      <p class="price-tag">
        <span class="product-price">{{
          formatPrice((product.price * product.discount) / 100)
        }}</span>
        <span class="discount-label">{{ product.discount }}%</span>
      </p>
      <span class="original-price">{{ formatPrice(product.price) }}</span>
    </div>
    <CartActions @add-to-cart="handleAddToCart" />
  </div>
</template>

<style scoped>
.product-details-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: start;
  gap: 2rem;
}

.product-brand {
  text-transform: uppercase;
  color: var(--clr-orange-500);
  font-size: 0.8125rem;
  font-weight: var(--fw-bold);
  letter-spacing: 2px;
  margin-bottom: 1.5rem;
}

.product-name {
  color: var(--clr-black);
  font-size: 2.75rem;
  font-weight: var(--fw-bold);
  line-height: 1.1;
}

.product-description {
  color: var(--clr-grey-500);
  font-weight: var(--fw-regular);
  font-size: 1rem;
  line-height: 1.7;
  margin-bottom: 1.5rem;
}

.price-tag {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.product-price {
  color: var(--clr-black);
  font-weight: var(--fw-bold);
  font-size: 1.75rem;
  letter-spacing: 1px;
}

.discount-label {
  background-color: var(--clr-orange-200);
  color: var(--clr-orange-500);
  font-weight: var(--fw-bold);
  padding: 0.25rem 0.5rem;
  border-radius: 0.25rem;
}

.original-price {
  display: block;
  color: var(--clr-grey-300);
  font-weight: var(--fw-bold);
  text-decoration: line-through;
  margin-top: 0.625rem;
}

@media screen and (max-width: 48rem) {
  .product-details-wrapper {
    padding: 2rem 1rem;
  }
}
</style>
