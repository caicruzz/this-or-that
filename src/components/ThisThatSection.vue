<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';

defineProps({
  options: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <div class="this-that-section">
    <card-option
        v-for="option in options"
        :key="option"
        :text="option.text"
    />
  </div>
</template>

<style scoped>
.this-that-section {
  display: flex;
  gap: 6%;
}

.dialog {
  background-color: #fff;
  border: white 1px solid;
}
</style>