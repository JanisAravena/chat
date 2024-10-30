<template>
  <div class="chat-box">
    <div
      v-for="(message, index) in messages"
      :key="index"
      :class="{'message': true, 'message-user1': message.user === user1, 'message-user2': message.user === user2}"
      :style="{ backgroundColor: message.color }"
    >
      <strong>{{ message.user.name.first }}:</strong> {{ message.text }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    messages: Array,
    user1: Object,
    user2: Object
  }
};
</script>

<style>
.chat-box {
  width: 50%;
  max-height: calc(4 * 80px + 5 * 16px); 
  overflow-y: auto;
  border-radius: 10px;
  padding: 20px;
  background-color: rgba(128, 128, 128, 0.5); 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.message {
  padding: 10px;
  margin: 8px 0;
  border-radius: 10px;
  color: #fff;
  font-size: 1.2em;
  font-weight: 500;
  display: inline-block;
  max-width: 80%;
  white-space: pre-wrap;
}

.message-user1 {
  align-self: flex-start;
}

.message-user2 {
  align-self: flex-end;
}

.message strong {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}
</style>