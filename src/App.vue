<template>
  <div class="app">
    <div class="user-profile">
      <UserProfile :user="user1" @sendMessage="sendMessage" />
    </div>
    
    <ChatBox :messages="messages" :user1="user1" :user2="user2" />
    
    <div class="user-profile">
      <UserProfile :user="user2" @sendMessage="sendMessage" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ChatBox from './components/ChatBox.vue';
import UserProfile from './components/UserProfile.vue';

export default {
  components: {
    ChatBox,
    UserProfile
  },
  data() {
    return {
      user1: null,
      user2: null,
      messages: []
    };
  },
  async created() {
    const [user1Data, user2Data] = await Promise.all([
      axios.get('https://randomuser.me/api/'),
      axios.get('https://randomuser.me/api/')
    ]);
    
    this.user1 = user1Data.data.results[0];
    this.user2 = user2Data.data.results[0];
  },
  methods: {
    sendMessage(message) {
      this.messages.push({ user: message.user, text: message.text, color: message.color });
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');

.app {
  display: flex;
  align-items: center; 
  justify-content: center;
  padding: 20px;
  gap: 20px;
  height: 100vh;
  box-sizing: border-box;
}

.user-profile {
  width: 25%;
  padding: 20px;
  background-color: #1e1e1e;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
  transition: transform 0.3s;
}

.user-profile:hover {
  transform: scale(1.05);
}

.chat-box {
  width: 50%;
  max-height: 70vh;
  overflow-y: auto;
  border-radius: 10px;
  padding: 20px;
  background-size: cover;
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
}

.message {
  padding: 10px;
  margin: 8px 0;
  border-radius: 10px;
  font-size: 1.5em;
  font-weight: 500;
  display: inline-block;
  max-width: 80%;
  white-space: pre-wrap;
  font-family: 'Roboto', sans-serif; 
}

.message strong {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
  font-family: 'Roboto', sans-serif;
}
</style>