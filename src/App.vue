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
        <input type="text" name="name" />
      </div>
    </div>
    <div class="valid-period">valid period component</div>
    <div class="triggers">triger component</div>
    <div class="filters">filter</div>
    <div class="actions">action component</div>
    <div class="footer">delete and save</div>
  </div>
</template>



<script setup>
import { NotebookPen } from "lucide-vue-next";
</script>



<style scoped lang="scss">
.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100vh;

  padding: 2rem;
  .header {
    .header-inner {
      display: flex;
      gap: 1rem;
      p {
        font-weight: bold;
      }
    }
  }
}
</style>
