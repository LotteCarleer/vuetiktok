
<script setup>
import { reactive, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = reactive([]);

onMounted(() => {
  fetch('https://lab5-p379.onrender.com/api/v1/messages/')
    .then(response => response.json())
    .then(data => {
      messages.push(...data);
    });
});


function addMessage(message) {
  fetch('https://lab5-p379.onrender.com/api/v1/messages/', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(message)
  })
    .then(response => {
      if (!response.ok) {
        throw new Error('Bericht versturen mislukt');
      }

      messages.unshift(message);
    })
    .catch(error => {
      console.log(error);
    });
}

</script>

<template>
  <div>
    <ChatMessages :messages="messages" />
    <ChatForm @send-message="addMessage" />
  </div>
</template>
