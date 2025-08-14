<script setup lang="ts">
import { ref, Transition } from 'vue';
import ShoppingCart from './ShoppingCart.vue';

const cartOpen = ref(false);
const mobileNavOpen = ref(false);

const { cartItems } = defineProps({
  cartItems: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <header>
    <div class="container container__header">
      <div class="header-left">
        <div class="logo-wrapper">
          <button @click="() => (mobileNavOpen = true)" class="mobile-nav-btn">
            <svg width="16" height="15" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M16 12v3H0v-3h16Zm0-6v3H0V6h16Zm0-6v3H0V0h16Z"
                fill="#69707D"
                fill-rule="evenodd"
              />
            </svg>
          </button>
          <a href="#"><img src="/images/logo.svg" alt="Sneakers" /></a>
        </div>
        <Transition>
          <nav v-if="mobileNavOpen" class="mobile-nav">
            <ul>
              <button
                @click="() => (mobileNavOpen = false)"
                class="close-mobile-nav-btn"
              >
                <svg width="14" height="15" xmlns="http://www.w3.org/2000/svg">
                  <path
                    d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
                    fill="#777777"
                    fill-rule="evenodd"
                  />
                </svg>
              </button>
              <li class="nav-link"><a href="#">Collection</a></li>
              <li class="nav-link"><a href="#">Men</a></li>
              <li class="nav-link"><a href="#">Women</a></li>
              <li class="nav-link"><a href="#">About</a></li>
              <li class="nav-link"><a href="#">Contact</a></li>
            </ul>
          </nav>
        </Transition>
        <nav class="main-nav">
          <ul>
            <li class="nav-link"><a href="#">Collection</a></li>
            <li class="nav-link"><a href="#">Men</a></li>
            <li class="nav-link"><a href="#">Women</a></li>
            <li class="nav-link"><a href="#">About</a></li>
            <li class="nav-link"><a href="#">Contact</a></li>
          </ul>
        </nav>
      </div>
      <div class="header-right">
        <button class="button-cart" @click="() => (cartOpen = !cartOpen)">
          <span class="sr-only">shopping cart</span>
          <svg
            class="header-cart-icon"
            width="22"
            height="20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
              fill="#69707D"
              fill-rule="nonzero"
            />
          </svg>
        </button>
        <button class="button-profile">
          <span class="sr-only">your profile</span>
          <img src="/images/image-avatar.png" alt="your profile" />
        </button>
      </div>
    </div>
    <ShoppingCart v-if="cartOpen" :cartItems="cartItems" />
  </header>
</template>

<style scoped>
.container__header {
  padding-inline: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid hsla(220, 14%, 75%, 0.5);
}

.logo-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.mobile-nav-btn {
  background-color: transparent;
  display: grid;
  place-items: center;
  display: none;
}

.main-nav > ul {
  display: flex;
  gap: 2rem;
  list-style-type: none;

  & li > a {
    display: inline-block;
    position: relative;
    text-decoration: none;
    font-weight: var(--fw-regular);
    color: var(--clr-grey-500);
    padding-block: 3rem;
    transition: all 0.3s ease-in-out;
  }

  & li > a::after {
    content: '';
    width: 100%;
    height: 4px;
    background-color: var(--clr-orange-500);
    position: absolute;
    bottom: 0;
    left: 0;
    opacity: 0;
    transition: all 0.3s ease-in-out;
  }

  & li > a:hover {
    color: var(--clr-black);
  }

  & li > a:hover::after {
    opacity: 1;
  }
}

.mobile-nav {
  background-color: hsla(0, 0%, 0%, 0.75);
  position: fixed;
  inset: 0;
  z-index: 999;

  & ul {
    max-width: 300px;
    width: 75%;
    height: 100%;
    background-color: white;
    padding: 1rem;
    list-style-type: none;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: start;
  }

  & ul > li > a {
    text-decoration: none;
    color: var(--clr-grey-700);
    font-weight: var(--fw-bold);
  }

  & ul > li > a:hover {
    opacity: 0.8;
  }
}

.close-mobile-nav-btn {
  background-color: transparent;
}

.header-left {
  display: flex;
  align-items: center;
  justify-content: start;
  gap: 3rem;
}

.header-left > * {
  flex-shrink: 0;
}

.header-right {
  display: flex;
  align-items: center;
  justify-content: end;
  gap: 1rem;
}

.header-cart-icon > path {
  transition: all 0.3s ease-in-out;
}

.header-cart-icon:hover > path {
  fill: var(--clr-black);
}

.button-profile {
  background-color: transparent;
  border: none;
  border-radius: 50%;
  width: 3rem;
  aspect-ratio: 1;
  border: 2px solid var(--clr-orange-500);
  border-color: transparent;
  transition: all 0.3s ease-in-out;
}

.button-profile:hover {
  border-color: var(--clr-orange-500);
}

.button-cart {
  background-color: transparent;
  border: none;
  width: 3rem;
  aspect-ratio: 1;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease-in-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

@media screen and (max-width: 48rem) {
  .container__header {
    border-bottom: none;
  }
  .mobile-nav-btn {
    display: grid;
  }

  .main-nav {
    display: none;
  }

  .header-right {
    gap: 0.5rem;
  }
}
</style>
