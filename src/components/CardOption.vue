<script setup lang="ts">

const { text, isActive, style } = defineProps({
  text: {
    type: String,
    required: true
  },
  isActive: {
    type: Boolean,
    default: false
  },
  style: {
    type: String,
    default: 'default-card'
  }
});

const emit = defineEmits(['toggleActive']);

function toggleActive() {
  emit('toggleActive', text);
}
</script>

<template>
  <div :class="'card ' + style" @click="toggleActive">
    <p :class="isActive ? 'active-text' : 'not-active-text'">{{ text }}</p>
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
