<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  },
  datetime: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="message">
    <h4>{{ msg }}</h4>
    <h6>{{ datetime }}</h6>
  </div>
</template>

<style scoped>
.message {
  padding: 8px;
  background-color: #555;
}
</style>
