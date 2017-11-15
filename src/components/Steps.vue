<template>
    <div :class="step.style" @click="$emit('goToStep', step.id)">
      {{ step.id }}
    </div>
</template>

<script>
  export default {
    props: {
      step: {
        type: Object,
        required: true
      }
    }
  }
</script>

<style scoped>
  .step {
    padding: 10px 15px 10px 15px;
    background: #ffffff;
    margin-right: 8px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    border-radius: 2px;
    cursor: pointer;
    opacity: 0.5;
  }

  .active {
    opacity: 1;
  }

  .passed {
    opacity: 1;
    color: #ff9800;
  }
</style>
