<script setup lang="ts">
import ThisThatSection from '@/components/ThisThatSection.vue';
import { onBeforeMount, ref } from 'vue';

const maxOptions = 5;
const isEditMode = ref(false);
const isDialogOpen = ref(false);
const optionsList = ref([
  { this: 'this', that: 'that', active: '' }
]);

onBeforeMount(() => {
  const options = localStorage.getItem('options');
  if (options) {
    optionsList.value = JSON.parse(options);
  }
});

function setIsDialogOpen(value: boolean) {
  isDialogOpen.value = value;
}

function addThisThatSection() {
  optionsList.value.push({ this: 'this', that: 'that', active: '' });
}

function removeThisThatSection(index: number) {
  optionsList.value.splice(index, 1);
}

function closeDialog() {
  const options = JSON.stringify(optionsList.value);
  localStorage.setItem('options', options);
  setIsDialogOpen(false);
}

function switchModes() {
  isEditMode.value = !isEditMode.value;
}
</script>

<template>
  <div class="home">
    <div class="heading">
      <h1>This or That</h1>
      <v-btn
      color="primary"
      @click="switchModes"
      >
        Switch to {{ isEditMode ? 'live' : 'edit' }} mode
      </v-btn>
    </div>
    <v-btn
    v-if="isEditMode"
      color="primary"
      @click="setIsDialogOpen(true)"
    >
      Edit Options
    </v-btn>
    <ThisThatSection
      v-for="(options, index) in optionsList"
      :key="index"
      :this-or-that="options"
      class="section"
    />
  </div>

  <v-dialog width="500" v-model="isDialogOpen">
    <v-card title="Edit your options">
      <v-btn
        color="primary"
        :disabled="optionsList.length >= maxOptions"
        @click="addThisThatSection()"
      >
        +
      </v-btn>
      <v-card-text>
        <div v-for="(options, index) in optionsList" :key="index" class="form-dialog">
          <v-text-field
            v-model="options.this"
            :label="options.this"
            required
          ></v-text-field>
          <v-text-field
              v-model="options.that"
              :label="options.that"
              required
          ></v-text-field>
          <v-btn color="primary" @click="removeThisThatSection(index)"> Delete </v-btn>
        </div>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          text="Close"
          :disabled="optionsList.length === 0"
          @click="closeDialog()"
        ></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style scoped>
.home {
  padding: 1rem 25rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
}

.section {
  margin: 20px 0;
}

.form-dialog {
  display: flex;
  gap: 1rem;
}

.heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
