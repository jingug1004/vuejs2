<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <message-list :items="messages" @delete="deleteMessage"></message-list>
    <ul>
      <li v-for="message in messages" v-bind:key="message">{{ message.text }} - {{ message.createdAt }}
        <button @click="deleteMessage(message)">delete</button>
      </li>
      <form v-on:submit.prevent="addMessage">
        <textarea v-model="newMessage" placeholder="Leave a message"></textarea>
        <div>
          <button v-bind:disabled="addDisabled" type="submit">Add
          </button>
        </div>
      </form>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      messages: [],
      newMessage: ''
    }
  },
  computed: {
    addDisabled () {
      return this.messages.length >= 4 || this.newMessage.length >= 5
    }
  },
  methods: {
    addMessage (event) {
      if (!this.newMessage) {
        return
      }
      this.messages.push({
        text: this.newMessage,
        createdAt: new Date()
      })
      this.newMessage = ''
    },
    deleteMessage (message) {
      this.messages.splice(this.messages.indexOf(message), 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
