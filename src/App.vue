<template>
  <div>
    <h1>Catatan Tugas</h1>
    <form @submit.prevent="addOrUpdateTodo">
      <input v-model="newTodo">
      <button v-if="!editMode">Tambah</button>
      <button v-else>Perbarui</button>
    </form>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done">
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(todo)">Hapus</button>
        <button @click="editTodo(todo)">Edit</button>
      </li>
    </ul>
    <button @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Tampilkan Semua Tugas' : 'Sembunyikan Tugas yang Selesai' }}
    </button>
  </div>
</template>

<script>
let id = 0;

export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      todos: [
        { id: id++, text: "Belajar JavaScript", done: true },
        { id: id++, text: "Belajar HTML", done: true },
        { id: id++, text: "Belajar Desaign", done: false }
      ],
      editMode: false,
      editingTodo: null
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.todos.filter((t) => !t.done) : this.todos;
    }
  },
  methods: {
    addOrUpdateTodo() {
      if (this.editMode) {
        this.editingTodo.text = this.newTodo;
        this.newTodo = "";
        this.editMode = false;
        this.editingTodo = null;
      } else {
        if (this.newTodo.trim() !== "") {
          this.todos.push({ id: id++, text: this.newTodo, done: false });
          this.newTodo = "";
        }
      }
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
    editTodo(todo) {
      this.editMode = true;
      this.editingTodo = todo;
      this.newTodo = todo.text;
    }
  }
};
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
~
<style>
.done {
  text-decoration: line-through;
}
.w1{
  justify-content: center;
  width: 500px;
  height: 500px;
  margin-top: 15%;
  margin-left: 40%;
}
body{
  justify-content: center;
background: url(https://wallpaperaccess.com/full/1249001.jpg) no-repeat center center fixed;
background-size: cover; 
}

h2{
  font-size: 15px;
}
</style>