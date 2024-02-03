<template>
  <!-- HTML -->
  <div>
    {{ str }}
    <app-header
        v-on:send-event="renewStr"
        v-bind:propsdata="str"></app-header>
    <form v-on:submit="submitForm">
      <div>
        <label for="username">id: </label>
        <input id="username" type="text" v-model="username">
      </div>
      <div>
        <label for="password">password: </label>
        <input id="password" type="password" v-model="password">
      </div>
      <button type="submit">login</button>
    </form>
  </div>
</template>

<script>
import AppHeader from "@/components/appHeader.vue";
import axios from 'axios';
export default {
  data: function () {
    return {
      str: 'Header',
      username: '',
      password: ''
    }
  },
  components: {
    'app-header': AppHeader
  },
  methods: {
    renewStr: function () {
      this.str = 'renewStr';
    },
    submitForm: function (event) {
      event.preventDefault();
      console.log(this.username, this.password)
      axios.post('https://jsonplaceholder.typicode.com/users', {
        username: this.username,
        password: this.password
      }).then(function (response){
        console.log(response)
      }).catch(function (error){
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>

</style>