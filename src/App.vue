<template>
  <div id="app">
    <h1>ChatGPTアプリ</h1>
    <ChatForm />
  </div>
</template>

<script>
import ChatForm from './components/ChatForm.vue';

export default {
  name: 'App',
  components: {
    ChatForm
  }
};
</script>

<style>
#app {
  text-align: center;
  padding: 20px;
}
</style>