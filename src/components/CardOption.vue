<template>
    <div class="card">
        <p>{{ text }}</p>
    </div>
</template>

<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
})
</script>

<style scoped>
.card {
  background-color: #fff;
  color: black;
  border-radius: 0.5rem;
  box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.075);
  padding: 1rem;
  text-align: center;
  text-overflow: wrap;
  font-size: 1.5rem;
  width: 12rem;
  height: 12rem;
  padding: 5% 0;
}
</style>
