<script setup lang="ts">
import { computed, ref } from 'vue';

type thisThatOptionType = {
  text: string;
  isActive: boolean;
  cardStyle: string;
}

type Props = {
  thisThatOption: thisThatOptionType;
}

const { thisThatOption } = defineProps<Props>();

const isCardActive = ref(thisThatOption.isActive);

const cardClass = computed(() => {
  return `card ${thisThatOption.cardStyle}`;
});

function toggleActive() {
  isCardActive.value = !isCardActive.value;
}
</script>

<template>
  <div :class="cardClass" @click="toggleActive">
    <p :class="isCardActive ? 'active-text' : 'not-active-text'">{{ thisThatOption.text }}</p>
  </div>
</template>

<style scoped>
.card {
  border-radius: 0.5rem;
  box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075);
  text-align: center;
  text-overflow: wrap;
  font-size: 1.5rem;
  width: 12rem;
  height: 12rem;
  padding: 3rem 0;
}

.default-card {
  background-color: #fff;
  color: black;
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

.disabled-card {
  background-color: rgb(177, 177, 177);
  color: rgb(177, 177, 177);
}
</style>
