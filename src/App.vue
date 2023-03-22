<template>
  <div class="container">
    <section>
      <h1>Todo list</h1>
      <p>What needs to be done ?</p>
      <form class="padding" @submit.prevent="addTodo">
        <input type="text" v-model="newTodo" />
        <button type="submit">Add new item</button>
      </form>
      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(todo)">delete</button>
        </li>
      </ul>
      <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? "Show all" : "Hide completed" }}
      </button>
    </section>
  </div>
</template>

<script>
let id = 0;
export default {
  data() {
    return {
      newTodo: "",
      hideCompleted: false,
      todos: [],
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
};
</script>

<style scoped>
* {
  text-transform: uppercase;
}
h1 {
  font-size: 2.5rem;
}
p {
  font-size: 1.5rem;
}
section {
  padding: 40px;
  color: #f2f2f2;
  letter-spacing: 1px;
}
form {
  margin-bottom: 33px;
  display: flex;
}
input[type="text"] {
  padding: 5px;
  font-size: 2rem;
  margin-right: 17px;
  background-color: gray;
}
input[type="text"]:focus {
  background-color: lightgray;
  box-shadow: 0px 0px 8px 5px lightgray;
}
input[type="checkbox"] {
  height: 20px;
  width: 20px;
}
ul {
  list-style: none;
  margin-bottom: 33px;
}
li {
  padding: 5px;
}
button {
  background-color: transparent;
  color: #f2f2f2;
  border: 1px solid gray;
  padding: 5px 10px;
  border-radius: 12px;
  cursor: pointer;
  letter-spacing: 1px;
}
button:hover {
  background-color: #f2f2f2;
  color: #222222;
}
span {
  padding: 15px;
  font-size: 1.5rem;
}
.done {
  text-decoration: line-through;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #222222;
  height: 100vh;
}
</style>
