<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';
import { computed } from 'vue';

type thisThatOption = {
  text: string;
  isActive: boolean;
  cardStyle: string;
}

type Props = {
  options: { this: thisThatOption, that: thisThatOption };
}

const mappedOptions = computed(() => {
  let mappedOptions = {
    this: { ...props.options.this, cardStyle: 'default-card' },
    that: { ...props.options.that, cardStyle: 'default-card'}
  };
  const isThisActive = props.options.this.isActive;
  const isThatActive = props.options.that.isActive;

  if (isThisActive) {
    mappedOptions.that.cardStyle = 'disabled-card';
  }

  if (isThatActive) {
    mappedOptions.this.cardStyle = 'disabled-card';
  }

  return mappedOptions;
});

const props = defineProps<Props>()
</script>

<template>
  <div class="this-that-section">
    <card-option
        v-for="option in mappedOptions"
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
