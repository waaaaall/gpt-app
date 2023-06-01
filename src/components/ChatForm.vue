<template>
  <div class="chat-form">
    <form @submit="handleSubmit">
      <input
        type="text"
        v-model="message"
        placeholder="Type a message..."
      />
      <button type="submit">Send</button>
    </form>
    <div class="response" v-if="response">{{ response }}</div>
  </div>
</template>

<script>
import { getChatGptResponse } from '../api';

export default {
  data() {
    return {
      message: '',
      response: ''
    };
  },
  methods: {
    async handleSubmit(event) {
      event.preventDefault();
      const prompt = this.message;
      this.message = '';
      try {
        const response = await getChatGptResponse(prompt);
        if (response && response.length > 0) {
          this.response = response;
        } else {
          this.response = 'No response received.';
        }
      } catch (error) {
        console.error(error);
        this.response = 'An error occurred. Please try again.';
      }
    }
  }
};
</script>

<style scoped>
.chat-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

form {
  display: flex;
  margin-bottom: 10px;
}

input[type='text'] {
  width: 300px;
  padding: 5px;
}

button {
  padding: 5px 10px;
}

.response {
  background-color: #f0f0f0;
  padding: 10px;
  border-radius: 5px;
}
</style>
