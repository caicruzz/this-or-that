<script setup lang="ts">
import { computed, ref, type PropType } from 'vue';

type thisThatOptionType = {
  text: string;
  isActive: boolean;
}

const { thisThatOption, style } = defineProps({
  thisThatOption: {
    type: Object as PropType<thisThatOptionType>,
    required: true
  },
  style: {
    type: String,
    default: 'default-card'
  }
});

const emit = defineEmits(['toggleActive']);

const isCardActive = ref(thisThatOption.isActive);

function toggleActive() {
  isCardActive.value = !isCardActive.value;
  emit('toggleActive');
}
</script>

<template>
  <div :class="'card ' + style" @click="toggleActive">
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
