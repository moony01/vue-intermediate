<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <BaseModal v-if="showModal" @close="showModal = false">
      <template v-slot:header>
        <h3>
          경고!
          <i class="closeModalBtn fa fa-times" @click="showModal = false">
        </i>
        </h3>
      </template>
      <template v-slot:body>
        <p>할 일을 입력하세요.</p>
      </template>
    </BaseModal>
  </div>
</template>

<script>
import BaseModal from './common/BaseModal.vue'

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        // this.$emit('addTodoItem', this.newTodoItem)
        this.$store.commit('addOneItem', this.newTodoItem);
        this.clearInput();
      } else {
        console.log("1");
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    BaseModal
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
