
<script setup>
defineProps({
  messages: Array
});
</script>

<template>
  <div class="messages">
    <div
      v-for="message in messages.slice(0, 20)"
      :key="message._id"
      class="message"
    >
      <strong>{{ message.user }}</strong>
      <p>{{ message.text }}</p>
    </div>
  </div>
</template>

<style scoped>

.messages {
  max-height: 250px;
  overflow-y: auto;
}

.message {
  padding: 8px;
  border-bottom: 1px solid #ddd;
}
</style>

