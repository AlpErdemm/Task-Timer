<script setup>
import TaskManager from './components/TaskManager.vue';
import Timer from './components/Timer.vue';
</script>

<template>
<div class="grid-container">
  <TaskManager />
  <Timer />
</div>
</template>

<style>
.grid-container {
  display: grid;
  grid-template-columns: auto auto;
  height: 800px;
  grid-gap: 10px;
  padding: 10px;
  column-gap: 50px;
  align-items: center;
}
body{
  background-color: rgb(224, 121, 121);
}
</style>
