<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';
import { ref, computed } from 'vue';

type thisThatOption = {
  text: string;
  isActive: boolean;
}

type Props = {
  options: { this: thisThatOption, that: thisThatOption };
}

const props = defineProps<Props>();
const thisOption = ref(props.options.this);
const thatOption = ref(props.options.that);

function onToggleActive(value: thisThatOption) {
  if (value.text === thisOption.value.text) {
    thisOption.value.isActive = !thisOption.value.isActive;
  } else if (value.text === thatOption.value.text) {
    thatOption.value.isActive = !thatOption.value.isActive;
  }
}

function getStyle(optionText: string) {
  const styleMap = new Map<string, string>();
  styleMap.set(thisOption.value.text, 'default-card');
  styleMap.set(thatOption.value.text, 'default-card');

  const isThisActive = thisOption.value.isActive;
  const isThatActive = thatOption.value.isActive;

  if (isThisActive) {
    styleMap.set(thatOption.value.text, 'disabled-card');
  } else if (isThatActive) {
    styleMap.set(thisOption.value.text, 'disabled-card');
  }

  return styleMap.get(optionText);
}
</script>

<template>
  <div class="this-that-section">
    <card-option
        :thisThatOption="thisOption"
        :style="getStyle(thisOption.text)"
        @toggleActive="onToggleActive(thisOption)"
    />
    <card-option
        :thisThatOption="thatOption"
        :style="getStyle(thatOption.text)"
        @toggleActive="onToggleActive(thatOption)"
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
