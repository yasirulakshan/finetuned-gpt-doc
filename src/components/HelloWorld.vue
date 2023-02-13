<template>
  <v-container>
    <v-row style="height: 500px;" justify="center">
      <v-col cols="8" >
        <v-sheet class="pa-2 rounded-lg" elevation="12">

          <v-card elevation="4">
            <div class="pa-4 text-center">
              <h3>{{ selectedOption }} <v-icon color="green">mdi-account-badge-outline</v-icon></h3>
            </div>
          </v-card>

          <div class="chat-messages">
            <v-row v-for="message in messages" :key="message.id" :justify="message.type === 'A' ? 'start' : 'end'" no-gutters>
              <div class="pa-3 mt-3 rounded-xl sm-12" :id="'chat-' + message.id" round="4" :style="{
                textAlign: message.type === 'A' ? 'start' : 'end',
                backgroundColor: message.type === 'A' ? '#FCF6F5FF' : '#FAEBEFFF'
              }"> <v-icon v-if="message.type === 'A'" color="green">mdi-account-badge-outline</v-icon> {{
  message.text
}} <v-icon v-if="message.type !== 'A'" color="green">mdi-chat</v-icon> </div>
            </v-row>
          </div>
          <div>
            <v-row class="pt-5" align="center">
              <v-col cols="11"><v-text-field variant="outlined" label="Type here" hide-details v-model="newMessageText"
                  required></v-text-field>
              </v-col>
              <v-col class="ml-5">
                <v-btn @click="getData" icon="mdi-send" color="primary"></v-btn>
              </v-col>
            </v-row>
            <v-row class="pb-5">
              <v-col cols="6">
                <v-select v-model="selectedOption" variant="outlined" :items="options" hide-details required
                  label="Choose the model"></v-select>
              </v-col>
            </v-row>
          </div>

        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

import axios from 'axios';
import anime from 'animejs/lib/anime.es.js';

export default {
  data() {
    return {
      messages: [
        { id: 1, type: "A", text: "Hello!" },
        { id: 2, type: "Q", text: "I'm good, thanks for asking." }
      ],
      options: ["Finetune AI Bot", "Base Model"],
      selectedOption: "Finetune AI Bot",
      newMessageText: ''
    };
  },
  methods: {
    addMessage() {

      this.messages.push({
        id: this.messages.length + 1,
        text: this.newMessageText,
        type: "Q"
      });

      this.newMessageText = "";
    },
    async getData() {

      await this.addMessage();

      anime({
        targets: '#chat-' + this.messages.length,
        scale: [0, 1],
        translateY: [100, 0],
        duration: 150,
        easing: 'easeOutQuad',
        autoplay: true
      });

      const response = await axios.get('https://jsonplaceholder.typicode.com/posts');


    }
  }
};
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200&display=swap');

* {
  font-family: 'Poppins', sans-serif;
}

.chat-messages {
  background-color: #9CC3D5FF;
  height: 60vh;
  overflow-y: scroll;
  padding: 10px;
}


.chat-messages::-webkit-scrollbar {
  width: 10px;
  background-color: #c9c9c9;
}

.chat-messages::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #467fa0;
}




</style>
