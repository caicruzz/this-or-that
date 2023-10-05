<script setup lang="ts">
import ThisThatSection from '@/components/ThisThatSection.vue';

</script>

<template>
  <div class="home">
    <ThisThatSection class="section" />
    <ThisThatSection class="section" />
  </div>
</template>

<style scoped>
.home {
  padding: 5% 30%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
}

.section {
  margin: 20px 0;
}
</style>
