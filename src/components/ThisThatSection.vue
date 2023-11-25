<script setup lang="ts">
import CardOption from '@/components/CardOption.vue';

type ThisOrThat = {
  this: string;
  that: string;
  active: string;
}

type Props = {
  thisOrThat: ThisOrThat
}

const { thisOrThat } = defineProps<Props>();

function onToggleActive(value: string) {
  thisOrThat.active = value;
}

function isActive(text: string) {
  return thisOrThat.active === text;
}

function getStyle(text: string) {
  if (!thisOrThat.active) return 'default-card';

  return isActive(text) ? 'default-card' : 'disabled-card';
}
</script>

<template>
  <div class="this-that-section">
    <card-option
        :text="thisOrThat.this"
        :style="getStyle(thisOrThat.this)"
        :is-active="isActive(thisOrThat.this)"
        @toggle-active="onToggleActive"
    />
    <card-option
        :text="thisOrThat.that"
        :style="getStyle(thisOrThat.that)"
        :is-active="isActive(thisOrThat.that)"
        @toggle-active="onToggleActive"
    />
  </div>
</template>

<style scoped>
.this-that-section {
  display: flex;
  gap: 6%;
}
</style>
