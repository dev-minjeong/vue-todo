<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>
    <Modal v-if="showModal" @close="showModal = false">
      <!--
      you can use custom content here to overwrite
      default content
    -->
      <h3 slot="header">
        Warn!
        <i
          class="closeModalBtn fa-solid fa-xmark"
          @click="showModal = false"
        ></i>
      </h3>
      <h2 slot="body">내용을 입력하세요.</h2>
      <div slot="footer">
        <p>copy right</p>
        <!-- <button>X</button> -->
      </div>
    </Modal>
  </div>
</template>

<script>
import Modal from "./common/Modal.vue";
export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false
    };
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== "") {
        //   this.$emit('이벤트이름', 인자1, 인자2, ...);
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function() {
      this.newTodoItem = "";
    }
  },
  components: {
    Modal: Modal
  }
};
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
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
  cursor: pointer;
}
</style>
