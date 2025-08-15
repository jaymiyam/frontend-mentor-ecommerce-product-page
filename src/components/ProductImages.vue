<script setup lang="ts">
import { ref } from 'vue';

const currentIndex = ref(0);

function loadPrevImage() {
  if (currentIndex.value === 0) return;
  currentIndex.value = currentIndex.value - 1;
}

function loadNextImage() {
  if (currentIndex.value >= images.length - 1) return;
  currentIndex.value = currentIndex.value + 1;
}

function goToImage(index: number) {
  if (index < 0 || index > images.length - 1) return;
  currentIndex.value = index;
}

const { images, thumbnails } = defineProps({
  images: {
    type: Object,
    required: true,
  },
  thumbnails: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['openModal']);
</script>

<template>
  <div>
    <div class="main-image-wrapper">
      <img
        class="main-image"
        :src="`images/${images[currentIndex]}`"
        :alt="images[0]"
      />
      <button @click="emit('openModal')" class="open-modal-btn">
        <span class="sr-only">open image gallery</span>
      </button>
      <div class="mobile-image-nav">
        <button @click="loadPrevImage" class="image-nav-btn prev">
          <svg width="12" height="18" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M11 1 3 9l8 8"
              stroke="#1D2026"
              stroke-width="3"
              fill="none"
              fill-rule="evenodd"
            />
          </svg>
        </button>
        <button @click="loadNextImage" class="image-nav-btn next">
          <svg width="13" height="18" xmlns="http://www.w3.org/2000/svg">
            <path
              d="m2 1 8 8-8 8"
              stroke="#1D2026"
              stroke-width="3"
              fill="none"
              fill-rule="evenodd"
            />
          </svg>
        </button>
      </div>
    </div>
    <div class="thumbnails-wrapper">
      <button
        @click="goToImage(parseInt(index))"
        class="thumbnail-image"
        v-for="(image, index) in thumbnails"
      >
        <img :src="`images/${image}`" :alt="image" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.main-image-wrapper {
  border-radius: 1rem;
  max-width: 28rem;
  overflow: hidden;
  margin-bottom: 2rem;
  position: relative;
}

.open-modal-btn {
  position: absolute;
  inset: 0;
  background-color: transparent;
  color: transparent;
}

.thumbnails-wrapper {
  max-width: 28rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  justify-content: space-between;
}

.thumbnail-image {
  max-width: 5.5rem;
  border-radius: 0.625rem;
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}

.thumbnail-image:hover {
  opacity: 0.7;
}

.mobile-image-nav {
  display: none;
}

.image-nav-btn {
  width: 48px;
  height: 48px;
  background-color: white;
  border-radius: 50%;
  display: grid;
  place-items: center;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.image-nav-btn.prev {
  left: 1rem;
}

.image-nav-btn.next {
  right: 1rem;
}

@media screen and (max-width: 48rem) {
  .main-image-wrapper {
    width: 100%;
    max-width: 100%;
    border-radius: 0;
    margin-bottom: 0;
  }

  .open-modal-btn {
    display: none;
  }

  .mobile-image-nav {
    display: block;
  }

  .thumbnails-wrapper {
    display: none;
  }
}
</style>
