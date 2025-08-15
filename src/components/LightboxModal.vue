<script setup lang="ts">
import { ref } from 'vue';

const currentIndex = ref(0);

const { thumbnails, images } = defineProps({
  thumbnails: {
    type: Object,
    required: true,
  },
  images: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['closeModal']);

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
</script>

<template>
  <dialog>
    <div class="modal-bg">
      <div class="modal-wrapper">
        <button class="modal-close-btn" @click="emit('closeModal')">
          <svg width="14" height="15" xmlns="http://www.w3.org/2000/svg">
            <path
              d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
              fill="#FFFFFF"
              fill-rule="evenodd"
            />
          </svg>
        </button>
        <div class="modal-main-image">
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
          <img :src="`images/${images[currentIndex]}`" alt="" />
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
        <div class="modal-thumbnails-wrapper">
          <button
            @click="goToImage(parseInt(index))"
            class="modal-thumbnail-image"
            v-for="(image, index) in thumbnails"
          >
            <img :src="`images/${image}`" :alt="image" />
          </button>
        </div>
      </div>
    </div>
  </dialog>
</template>

<style scoped>
dialog {
  all: unset;
  position: fixed;
  inset: 0;
}

.modal-bg {
  width: 100%;
  height: 100%;
  background-color: hsla(0, 0%, 0%, 0.8);
  display: grid;
  place-items: center;
}

.modal-close-btn {
  background: transparent;
  align-self: end;
}

.modal-wrapper {
  /* width: 600px; */
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
}

.modal-main-image {
  width: 500px;
  overflow: hidden;
  position: relative;
  display: grid;
  place-items: center;
}

.modal-main-image > img {
  max-width: 420px;
  border-radius: 1rem;
}

.image-nav-btn {
  width: 56px;
  height: 56px;
  background-color: white;
  border-radius: 50%;
  display: grid;
  place-items: center;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.image-nav-btn.prev {
  left: 0;
}

.image-nav-btn.next {
  right: 0;
}

.modal-thumbnails-wrapper {
  width: 420px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.modal-thumbnail-image {
  width: 5.5rem;
  border-radius: 0.625rem;
  border: 2px solid transparent;
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}

.modal-thumbnail-image:hover {
  border-color: var(--clr-orange-500);
}
</style>
