<script setup lang="ts">
import ThisThatSection from '@/components/ThisThatSection.vue';
import { onMounted, ref } from 'vue';

type thisThatOption = {
  text: string;
  isActive: boolean;
};

type options = {
  this: thisThatOption;
  that: thisThatOption;
};

const maxOptions = 5;
const isDialogOpen = ref(false);
const optionsList = ref<options[]>([
  {
    this: { text: 'This', isActive: false },
    that: { text: 'That', isActive: false }
  }
]);

onMounted(() => {
  const options = localStorage.getItem('options');
  if (options) {
    optionsList.value = JSON.parse(options);
  }
});

function setIsDialogOpen(value: boolean) {
  isDialogOpen.value = value;
}

function addThisThatSection() {
  optionsList.value.push({
    this: { text: 'This', isActive: false },
    that: { text: 'That', isActive: false }
  });
}

function removeThisThatSection(index: number) {
  optionsList.value.splice(index, 1);
}

function closeDialog() {
  const options = JSON.stringify(optionsList.value);
  localStorage.setItem('options', options);
  setIsDialogOpen(false);
}
</script>

<template>
  <div class="home">
    <v-btn color="primary" @click="setIsDialogOpen(true)"> Edit Options </v-btn>
    <ThisThatSection
      v-for="(options, index) in optionsList"
      :key="index"
      :options="options"
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
            v-for="(option, index) in options"
            :key="index"
            v-model="option.text"
            :label="option.text"
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
</style>
