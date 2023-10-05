<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';

const options = [
  'this',
  'that',
];
</script>

<template>
  <div class="this-that-section">
    <card-option
        v-for="option in options"
        :key="option"
        :text="option"
    />
  </div>
</template>

<style scoped>
.this-that-section {
  display: flex;
  gap: 6%;
}
</style>