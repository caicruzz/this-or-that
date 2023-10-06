<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';

type thisThatOption = {
  text: string;
  isActive: boolean;
}

type Props = {
  options: { this: thisThatOption, that: thisThatOption };
}

const props = defineProps<Props>()
</script>

<template>
  <div class="this-that-section">
    <card-option
        v-for="option in props.options"
        :key="option.text"
        :thisThatOption="option"
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
