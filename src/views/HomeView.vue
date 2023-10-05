<script setup lang="ts">
import ThisThatSection from '@/components/ThisThatSection.vue';
import {ref} from "vue";

const isDialogOpen = ref(false);

const optionsList = ref([
  {
    This: { text: 'This' },
    That: { text: 'That' },
  },
]);

function setIsDialogOpen(value: boolean) {
  isDialogOpen.value = value
}
</script>

<template>
  <div class="home">
    <v-btn
        color="primary"
        @click="setIsDialogOpen(true)"
    >
      Edit Options
    </v-btn>
    <ThisThatSection
        v-for="(options, index) in optionsList"
        :key="index"
        :options="options"
        class="section"
    />
  </div>

  <v-dialog width="500" v-model="isDialogOpen">
    <v-card title="Edit your options">
      <v-card-text>
          <div
              v-for="(options, index) in optionsList"
              :key="index"
              class="form-dialog"
          >
              <v-text-field
                  v-for="(option, index) in options"
                  :key="index"
                  v-model="option.text"
                  :label="option.text"
                  required
              ></v-text-field>
          </div>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
            text="Close Dialog"
            @click="setIsDialogOpen(false)"
        ></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
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

.form-dialog {
  display: flex;
}
</style>
