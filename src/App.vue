<script setup>
</script>

<template>
  <div class="wrapper">
    <div class="header">
      <div class="header-inner">
        <NotebookPen />
        <p>Create automated action</p>
      </div>
      <div class="name">
        <p>Name:</p>
        <input type="text" name="name" v-model="name" />
      </div>
      <div class="enabled">
        <p>Enabled</p>
        <input type="checkbox" v-model="enabled" />
      </div>
    </div>
    <div class="valid-period">
      <Valid @dateChange="handleDateChange" />
    </div>
    <div class="triggers">
      <Trigger @triggerEmits="setTrigerOptions" />
    </div>
    <div class="filters">
      <Filter @filterEmit="updateFilters" />
    </div>
    <div class="actions">
      <Action @actionEmit="someAction" />
    </div>
    <div class="footer">delete and save</div>
  </div>
</template>



<script setup>
import { NotebookPen } from "lucide-vue-next";
import { ref } from "vue";
import Valid from "@/components/Valid.vue";
import Trigger from "@/components/Trigger.vue";
import Filter from "@/components/Filter.vue";
import Action from "@/components/Action.vue";

const name = ref("");
const enabled = ref(false);
const startDate = ref(null);
const endDate = ref(null);
const triger = ref({});
const filterOptions = ref({});

function handleDateChange(dates) {
  startDate.value = dates.startDate;
  endDate.value = dates.endDate;

  console.log(startDate.value, endDate.value, "this are emited dates");
}

function setTrigerOptions(options) {
  triger.value = options;
  console.log(triger.value, "kajnsdkjsnd");
}

function updateFilters(filterValues) {
  filterOptions.value = filterValues;
  console.log(filterOptions.value, "filter options");
}

const actionData = ref({});

function someAction(data) {
  actionData.value = data;
  console.log(actionData.value, "this is action data to send to backend later");
}
</script>



<style scoped lang="scss">
.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
  // height: 100vh;
  gap: 2rem;
  padding: 2rem;
  .header {
    .header-inner {
      display: flex;
      gap: 1rem;
      p {
        font-weight: bold;
      }
    }
    .name {
      display: flex;
      justify-content: space-between;
    }
  }
}
</style>
