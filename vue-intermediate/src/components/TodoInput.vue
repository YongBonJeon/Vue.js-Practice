<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus"></i>
    </span>

    <modal :show="showModal" @close="showModal = false">
        <h3 slot="header">
          경고!
          <i class="closeModalBtn fa-solid fa-xmark " @click="showModal = false"></i>
        </h3>
        <p slot="body">할 일을 입력해주세요.</p>

    </modal>
  </div>
</template>

<script>
import Modal from "./common/MyModal.vue";
export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem === '') {
        this.showModal = true;
        return;
      }
      this.$store.commit('addOneItem', this.newTodoItem);
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>
