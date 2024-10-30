<template>
    <div class="profile">
      <img :src="user.picture.large" :alt="user.name.first" class="profile-picture" />
      <h3 class="profile-name">{{ user.name.first }} {{ user.name.last }}</h3>
      <div class="input-container">
        <input v-model="messageText" placeholder="Escribe un mensaje..." class="input-message" />
        <button @click="toggleEmojiPicker" class="emoji-button">😊</button>
      </div>
      <input type="color" v-model="messageColor" class="input-color" />
      <emoji-picker v-if="showEmojiPicker" @emoji-click="addEmoji"></emoji-picker>
      <button @click="send" class="send-button">Enviar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      user: Object
    },
    data() {
      return {
        messageText: '',
        messageColor: 'black',
        showEmojiPicker: false
      };
    },
    methods: {
      send() {
        if (this.messageText.trim()) {
          this.$emit('sendMessage', { user: this.user, text: this.messageText, color: this.messageColor });
          this.messageText = '';
        }
      },
      addEmoji(event) {
        this.messageText += event.detail.unicode;
      },
      toggleEmojiPicker() {
        this.showEmojiPicker = !this.showEmojiPicker;
      }
    }
  };
  </script>
  
  <style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');

  .profile {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 20px;
    background-color: #1e1e1e;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
    transition: transform 0.3s;
    font-family: 'Roboto', sans-serif; 
  }
  
  .profile:hover {
    transform: scale(1.05);
  }
  
  .profile-picture {
    width: 80%;
    max-width: 150px;
    border-radius: 50%;
    margin-bottom: 10px;
  }
  
  .profile-name {
    font-size: 1.2em;
    font-weight: bold;
    color: #ffffff;
    margin: 10px 0;
    font-family: 'Roboto', sans-serif; 
  }
  
  .input-container {
    display: flex;
    align-items: center;
    width: 100%;
  }
  
  .input-message {
    flex: 1;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #333;
    border-radius: 5px;
    box-sizing: border-box;
    background-color: #333;
    color: #ffffff;
    font-family: 'Roboto', sans-serif;
  }
  
  .emoji-button {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1.5em;
    margin-left: 10px;
    color: #ffffff;
    font-family: 'Roboto', sans-serif;
  }
  
  .input-color {
    margin-bottom: 10px;
    cursor: pointer;
  }
  
  .send-button {
    padding: 10px 20px;
    background-color: #4a90e2;
    color: #ffffff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-family: 'Roboto', sans-serif; 
  }
  
  .send-button:hover {
    background-color: #357abd;
  }
  </style>