<template>
  <v-container>
      <v-row style="height: 500px;">
        <v-col>
          <v-sheet class="pa-2 rounded-lg" elevation="12">
            <div class="chat-container">
              <div class="chat-header">
                <h3>Finetune AI Bot</h3>
              </div>
              <div class="chat-messages">
                <ul>
                  <li v-for="message in messages" :key="message.id" :style="{
                    backgroundColor: message.type === 'A' ? '#FCF6F5FF' : '#FAEBEFFF',
                    textAlign : message.type === 'A' ? 'left' : 'right'
                    }">
                    <p>{{ message.text }}</p>
                  </li>
                </ul>
              </div>
              <div class="chat-input">
                <input type="text" v-model="newMessageText" @keyup.enter="addMessage" />
                <button @click="addMessage">Send</button>
              </div>
            </div>
          </v-sheet>
        </v-col>
      </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      messages: [
        { id: 1, type:"A", text: "Hello!" },
        { id: 2, type:"A", text: "How are you?" },
        { id: 3, type:"Q", text: "I'm good, thanks for asking." }
      ],
      newMessageText: ""
    };
  },
  methods: {
    addMessage() {
      this.messages.push({
        id: this.messages.length + 1,
        text: this.newMessageText
      });
      this.newMessageText = "";
    }
  }
};
</script>


<style>
/* *{
  border:1px solid black;
} */
.chat-container {
  width: 100%;
  margin: 0 auto;
}

.chat-header {
  background-color: #5B84B1FF;
  padding: 10px;
  text-align: center;
}

.chat-messages {
  background-color: #9CC3D5FF;
  height: 70vh;
  overflow-y: scroll;
  padding: 10px;
}

.chat-messages ul li{
  margin-bottom: 5px;;
}

.chat-input {
  background-color: #5B84B1FF;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

.chat-input input[type="text"] {
  flex: 1;
  padding: 5px;
  background-color: #9CC3D5FF;
}

.chat-input button {
  padding: 5px 10px;
  background-color: #9CC3D5FF;
  margin-left: 5px;
}
</style>
