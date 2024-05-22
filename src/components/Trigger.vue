<template>
  <div class="trigger-wrapper">
    <div class="header">
      <p>Trigger</p>
      <select v-model="selectedOption" @change="optionChanged">
        <option value="Daily">Daily</option>
        <option value="Scheduled">Scheduled (time)</option>
        <option value="Points Changed">Points Changed</option>
        <option value="Manual booking">Manual booking</option>
        <option value="Reward redeemed">Reward redeemed</option>
        <option value="Participated in sweepstake">
          Participated in sweepstake
        </option>
        <option value="Check-in">Check-in</option>
        <option value="Purchase redeemed">Purchase redeemed</option>
        <option value="Coupon redeemed">Coupon redeemed</option>
      </select>
    </div>
    <div v-if="selectedOption === 'Scheduled'" class="select-schedule">
      <p>Enter time:</p>
      <input type="time" v-model="scheduledTime" @input="optionChanged" />
      <p>Select frequency:</p>
      <select v-model="frequency" @click="optionChanged">
        <option value="Daily">Daily</option>
        <option value="Weekly">Weekly</option>
        <option value="Monthly">Monthly</option>
      </select>
    </div>
    <div class="max-frequency">
      <p>Max frequence</p>
      <div>
        <p>Only once:</p>
        <input type="checkbox" v-model="onlyOnce" @click="optionChanged" />
      </div>
      <div class="wrapper" v-if="!onlyOnce">
        <p>Days</p>
        <input type="text" v-model="maxFrequency" @input="optionChanged" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["triggerEmits"]);

const selectedOption = ref("Daily");
const scheduledTime = ref("");
const frequency = ref("Daily");
const maxFrequency = ref(null);
const onlyOnce = ref(false);

const optionChanged = () => {
  if (onlyOnce.value) {
    maxFrequency.value = "1";
  }
  if (selectedOption.value === "Scheduled") {
    emit("triggerEmits", {
      option: selectedOption.value,
      time: scheduledTime.value,
      frequency: frequency.value,
      maxFrequency: maxFrequency.value,
    });
  } else {
    emit("triggerEmits", {
      option: selectedOption.value,
      maxFrequency: maxFrequency.value,
    });
  }
};
</script>

<style scoped lang="scss">
.trigger-wrapper {
  margin-top: 20px;
  display: grid;
  gap: 2rem;
}
.header {
  margin-bottom: 10px;
}

.select-schedule {
  display: flex;
  justify-content: space-between;
}

.max-frequency {
  display: flex;
  gap: 3rem;
}
</style>
