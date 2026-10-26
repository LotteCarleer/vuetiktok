
<script setup>
import { ref } from 'vue';

const user = ref('');
const text = ref('');

const emit = defineEmits(['send-message']);

function submitMessage() {
  emit('send-message', {
    user: user.value,
    text: text.value
  });

  text.value = '';
}
</script>

<template>
  <form @submit.prevent="submitMessage">
    <input v-model="user" placeholder="Je naam" required />
    <input v-model="text" placeholder="Je reactie" required />
    <button type="submit">Versturen</button>
  </form>
</template>
