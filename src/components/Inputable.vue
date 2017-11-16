<template>
  <div class="inputWrapper">
    <input
      :class="formable.notValid"
      v-model.trim="formable.value"
      :type="formable.type"
      :placeholder="formable.placeholder"
      :title="formable.title"
    >
    <span v-if="formable.valid">{{ formable.error }}</span>
  </div>
</template>

<script>
  export default {
    props: {
      formable: {
        type: Object,
        required: true
      }
    }
  }
</script>

<style scoped>
  .inputWrapper span {
    display: inline-block;
    margin: 25px 0 0 0;
    color: #ff0000;
  }

  input[type="text"].notValid {
    border: 1px solid #ff0000;
  }

  input[type="text"] {
    font-family: "Open Sans", sans-serif;
    font-size: 15px;
    padding: 12px;
    margin-top: 16px;
    border: 0;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    border-radius: 2px;
    width: 20em;
  }

  input[type="text"]::placeholder {
    font-family: "Open Sans", sans-serif;
    color: #bbbbbb;
  }
</style>
