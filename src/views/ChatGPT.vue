<script>
import * as Vue from 'vue'
import axios from 'axios'
import moment from 'moment'
import MessageGPT from '../components/MessageGPT.vue'
import MessageMe from '../components/MessageMe.vue'

export default {
  data() {
    return {
      title: '正在输入...'
    }
  },
  methods: {
    onSend() {
      let msg = this.$refs.input_box.textContent
      this.$refs.input_box.textContent = ''

      if (msg.trim().length === 0) {
        return
      }

      const insertMessage = (content, bgColor) => {
        const node = document.createElement('div');
        node.style.padding = '8px'
        node.style.backgroundColor = bgColor
        node.innerText = content
        this.$refs.output_box.appendChild(node);
        this.$refs.output_box.scrollTop = this.$refs.output_box.scrollHeight
      }

      const template = `<MessageMe msg="${msg} datetime="${moment().format('YYYY-MM-DD HH:mm:ss')}" />`;
      insertMessage(msg, "#555555")

      const data = {
        "model": "gpt-3.5-turbo",
        "messages": [{ "role": "user", "content": `${msg}` }]
      }

      const config = {
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${localStorage.getItem('APP_KEY')}`,
        }
      }

      axios.post('https://api.openai.com/v1/chat/completions', JSON.stringify(data), config)
        .then(response => {
          let data = response.data
          const template = `<MessageMe msg="${data} datetime="${moment().format('YYYY-MM-DD HH:mm:ss')}" />`;
          insertMessage(data.choices[0].message.content.trim(), "#00000000")
        })
        .catch(error => {
          console.log(error)
        })
    }
  },
  mounted() {

  }
}
</script>

<template>
  <div class="container">
    <div class="output">
      <div class="title"><img alt="Vue logo" src="@/assets/logo.svg" />
        <h3>{{ title }}</h3>
      </div>
      <div class="content" ref="output_box"></div>
    </div>
    <div class="input">
      <div id="text" contenteditable="true" ref="input_box"></div>
      <button @click="onSend">发送</button>
    </div>
  </div>
</template>

<style>
.container {
  flex: 0.96;
  height: calc(100% - 16px);
  margin-top: auto;
  margin-bottom: auto;
  border-radius: 8px;
  background-color: #333;
}

.output {
  width: inherit;
  height: 94%;
}

.title {
  display: flex;
  padding: 8px;
  align-items: center;
}

.title img {
  float: left;
  width: 20px;
  height: 20px;
  margin-right: 2px;
}

.content {
  width: inherit;
  height: inherit;
  overflow-y: auto;
}

.chatgpt {
  padding: 8px;
  background-color: #555;
}

.input {
  overflow-y: auto;
  width: auto;
  height: 30px;
  margin-top: 8px;
  margin-left: 15px;
  margin-right: 15px;
  border-radius: 30px;
  border: 1px solid #666;
}

.input #text {
  float: left;
  width: calc(100% - 49px);
  height: 100%;
  display: flex;
  align-items: center;
  padding-left: 8px;
  padding-right: 8px;
  border-radius: 30px;
  border: 0px solid #666;
}

.input #text:focus {
  outline: none;
}

.input button {
  width: 45px;
  height: 24px;
  margin-left: 2px;
  border-radius: 30px;
  border: 0px solid #666;
  background-color: hsla(160, 100%, 37%, 1);
  color: #eee;
}
</style>
