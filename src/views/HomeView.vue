<script setup lang="ts">
import CardOption from '../components/CardOption.vue';

const options = [
  'this',
  'that',
];
</script>

<template>
    <div class="home">
        <div class="options">
            <card-option v-for="option in options" :key="option" :text="option" />
        </div>
    </div>
</template>

<style scoped>
.home {
  display: flex;
  height: 100%;
}
</style>
