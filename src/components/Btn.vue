<template>
  <div class="buttonWrapper">
    <span :class="btn.prevClass" @click="$emit('getPrev')">
      <i class="fa fa-angle-left" aria-hidden="true"></i>
      {{ btn.prev }}
    </span>
    <span :class="btn.nextClass" @click="$emit('getNext')">
      {{ btn.next }}
      <i v-if="btn.nextClass !== 'finish'" class="fa fa-angle-right" aria-hidden="true"></i>
    </span>
  </div>
</template>

<script>
  export default {
    props: {
      btn: {
        type: Object,
        required: true
      }
    }
  }
</script>

<style>
  .buttonWrapper {
    margin: 150px 0 0 0;
    display: inline-flex;
    color: #ff9800;
  }

  .buttonWrapper span {
    padding: 10px 15px 10px 15px;
    background: #ffffff;
    margin-right: 16px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    border-radius: 2px;
    cursor: pointer;
    font-weight: bold;
  }

  .disabled {
    opacity: 0.5;
  }

  span.finish {
    background: #ff9800;
    color: #ffffff;
    text-align: center;
  }

  span.off {
    display: none;
  }
</style>
