<template>
  <div class="chatbot">
    <div class="chatbot-window">
      <div class="messages">
        <div v-for="(msg, index) in messages" :key="index" :class="msg.sender">
          {{ msg.text }}
        </div>
      </div>
      <input v-model="userInput" @keyup.enter="sendMessage" placeholder="Ask me anything...">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInput: '',
      messages: [
        { text: 'Hello! Ask me anything about myself.', sender: 'bot' }
      ]
    };
  },
  methods: {
    sendMessage() {
      const text = this.userInput.trim();
      if (text) {
        this.messages.push({ text, sender: 'user' });
        this.userInput = '';
        this.processMessage(text);
      }
    },
    processMessage(text) {
      let response = '';
      switch (text.toLowerCase()) {
        case 'Where did you graduate?':
          response = 'I graduated from National University of Science & Technology.';
          break;
        case 'When did you graduate?':
          response = 'I graduated in July, 2023';
          break;
        case 'Which bachelor degree you did?':
          response = 'I did bachelors in Computer Sciences';
          break;
        case 'Where do you live?':
          response = 'I live in Lahore, Pakistan.';
          break;
        case 'What is your work experience?':
          response = 'I have 1 years of experience as a Full Stack Developer.';
          break;
        case 'What is your Stack in Web Developement?':
          response = 'My Stack is MERN Stack, also I can work on vueJS and Django.';
          break;
        case 'What Frontend Technologies are you currently working on?':
          response = 'I am working on ReactJS, VueJS, AngularJS, HTML5, CSS, Bootstrap, TailwindCSS.';
          break;
        case 'when did you start professional work?':
          response = 'I started my professional career in 2024.';
          break;
        default:
          response = 'I am not sure how to answer that. Can you ask something else?';
      }
      this.messages.push({ text: response, sender: 'bot' });
    }
  }
};
</script>

<style>
.chatbot {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 300px;
  background-color: white;
  border: 1px solid #ccc;
}
.chatbot-window {
  display: flex;
  flex-direction: column;
  height: 400px;
  padding: 10px;
}
.messages {
  flex: 1;
  overflow-y: auto;
}
.messages .user {
  text-align: right;
  margin: 5px 0;
}
.messages .bot {
  text-align: left;
  margin: 5px 0;
}
input {
  border: 1px solid #ccc;
  padding: 5px;
  width: calc(100% - 10px);
}
</style>
