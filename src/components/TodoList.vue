<template>
  <div class="hello">
    <input
      class="new-todo"
      autofocus
      autocomplete="off"
      placeholder="Add Todo"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <ul>
      <Todo
        v-for="todo in todos"
        :key="todo.id"
        v-bind:todo="todo"
        v-on:check-todo="check($event, todo.id)"
        v-on:edit-todo="editTodo()"
        v-on:delete-todo="deleteTodo(todo.id)"
      />
    </ul>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: "TodoList",
  components: {
    Todo,
  },
  data() {
    return {
      newTodo: "",
      todos: JSON.parse(localStorage.getItem("todoList")) || [],
    };
  },
  methods: {
    addTodo: function() {
      if (!this.newTodo) {
        return;
      }
      let obj = {
        id: Math.random(),
        text: this.newTodo.trim(),
      };
      this.todos.push(obj);
      localStorage.setItem("todoList", JSON.stringify(this.todos));
      this.newTodo = "";
    },
    check: function(event, todoId) {
      let todoIndex = this.todos.findIndex((el) => el.id == todoId);
      if (event.target.checked) {
        this.todos[todoIndex].completed = true;
      } else {
        this.todos[todoIndex].completed = false;
      }
      localStorage.setItem("todoList", JSON.stringify(this.todos));
    },
    editTodo: function() {
      localStorage.setItem("todoList", JSON.stringify(this.todos));
    },
    deleteTodo: function(todoId) {
      let filteredArray = this.todos.filter((el) => el.id != todoId);
      this.todos = [...filteredArray];
      localStorage.setItem("todoList", JSON.stringify(this.todos));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
.new-todo{
    padding: 10px 15px;
    border: 1px solid #888;
    outline: 0;
    box-shadow: none;
    border-radius: 4px;
    width: 80%;
}
</style>
