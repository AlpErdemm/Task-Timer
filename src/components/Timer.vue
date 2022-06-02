<script>
  export default {
    props: {
      duration: Number,
      continue: Boolean,
    },
  }
</script>

<template>
  <div :class="$style.container">
    <h1 v-if="this.duration === 0">Finished!</h1>
    <div v-else>
      <h1>{{`${Math.floor(duration / 60)} : ${(duration % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })}`}}</h1>
      <button @click="this.$emit('toggleInterval')">
        {{ this.continue ? 'Stop' : 'Start' }}
      </button>
    </div>
  </div>
</template>

<style module>
  .container {
    color: white;
    text-align: center;
  }
</style>
