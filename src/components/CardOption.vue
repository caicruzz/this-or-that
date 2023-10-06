<script setup lang="ts">
import { ref } from 'vue';

type thisThatOptionType = {
  text: string;
  isActive: boolean;
}

type Props = {
  thisThatOption: thisThatOptionType;
}

const { thisThatOption } = defineProps<Props>();

const isCardActive = ref(thisThatOption.isActive);

function toggleActive() {
  isCardActive.value = !isCardActive.value;
}
</script>

<template>
  <div class="card" @click="toggleActive">
    <p :class="isCardActive ? 'active-text' : 'not-active-text'">{{ thisThatOption.text }}</p>
  </div>
</template>

<style scoped>
.card {
  background-color: #fff;
  color: black;
  border-radius: 0.5rem;
  box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075);
  text-align: center;
  text-overflow: wrap;
  font-size: 1.5rem;
  width: 12rem;
  height: 12rem;
  padding: 3rem 0;
}

@keyframes showOption {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.active-text {
  animation: showOption 0.5s ease-in-out;
}

.not-active-text {
  display: none;
}

.not-active-card {
  display: none;
}
</style>
