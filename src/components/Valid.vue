<template>
  <div class="valid-wrapper">
    <div class="from">
      <p>Valid from</p>
      <input type="date" v-model="startDate" @change="emitDateChange" />
    </div>
    <div class="till">
      <p>Valid till</p>
      <input type="date" v-model="endDate" @change="emitDateChange" />
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const startDate = ref(null);
const endDate = ref(null);

const emit = defineEmits(["dateChange"]);

const emitDateChange = () => {
  emit("dateChange", { startDate: startDate.value, endDate: endDate.value });
};
</script>

<style scoped lang="scss">
.valid-wrapper {
  display: flex;
  justify-content: space-between;
}
</style>
