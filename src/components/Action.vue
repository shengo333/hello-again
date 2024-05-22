<template>
  <div class="action-wrapper">
    <div>
      <p>Select action</p>
      <select v-model="selectedAction">
        <option v-for="action in actions" :value="action" :key="action">
          {{ action }}
        </option>
      </select>
    </div>
    <div class="option-wrapper">
      <!-- Inputs for selected action -->
      <div v-if="selectedAction === 'Send message'" class="action-options">
        <div>
          <p>Channel:</p>
          <select v-model="selectedOption" @change="optionChanged">
            <option value="Daily">Daily</option>
            <option value="temporary">temporary</option>
            <option value="work">work</option>
          </select>
        </div>
        <div class="wrapper">
          <span>
            <label for="message">Message Title</label>
            <input
              type="text"
              placeholder="Enter message"
              v-model="message"
              @input="emitAction"
            />
          </span>
          <span>
            <label for="main">Text</label>
            <textarea name="text" id="" cols="30" rows="10"></textarea>
          </span>
        </div>
      </div>
      <div v-if="selectedAction === 'Create Task'" class="action-options">
        <p>Task Name</p>
        <input
          type="text"
          placeholder="Enter task name"
          v-model="taskName"
          @input="emitAction"
        />
      </div>
      <!-- Add more options for other actions as needed -->
    </div>
    <button @click="performAction" class="perform-action">
      Perform Action
    </button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const selectedOption = ref(null);

const actions = ref(["Send message", "Create Task"]); // Add more actions as needed
const selectedAction = ref(null); // Initialize with null

// Input values for different selected action
let message = ref("");
let taskName = ref("");

// Emit action event
const emitAction = () => {
  const actionData = {
    action: selectedAction.value,
    message: selectedAction.value === "Send message" ? message.value : null,
    taskName: selectedAction.value === "Create Task" ? taskName.value : null,
    // Add more data for other actions as needed
  };
  emit("actionEmit", actionData);
};

function performAction() {
  emitAction();
}

const emit = defineEmits(["actionEmit"]);
</script>

<style scoped lang="scss">
.wrapper {
  display: flex;
  gap: 1rem;
  span {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
}

.action-wrapper {
  margin-top: 20px;
}

.action-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.action-options {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 1rem;
}

.perform-action {
  background: lightblue;
  padding: 1rem;
  max-width: 10rem;
  border: none;
  border-radius: 15px;
}
</style>
