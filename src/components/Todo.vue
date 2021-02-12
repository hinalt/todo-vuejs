<template>
  <li class="todo" :class="{ completed: todo.completed }">
    <div class="todo-title">
      <input
        type="checkbox"
        name="todo.id"
        v-model="todo.completed"
        v-on:change="$emit('check-todo', $event)"
      />
      <input
        type="text"
        v-model="todo.text"
        class="text"
        v-on:blur="$emit('edit-todo')"
        v-on:keyup.enter="$emit('edit-todo')"
      />
    </div>
    <span class="remove" v-on:click="$emit('delete-todo')">X</span>
  </li>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {
      type: Object,
    },
  },
};
</script>

<style scoped>
li {
  margin: 0 10px;
}
.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-align: left;
  padding: 10px 20px;
  border-bottom: 1px solid #eee;
}
.todo-title{
  display: flex;
  align-items: center;
  width: 95%;
}
.remove {
  display: none;
  float: right;
  cursor: pointer;
  padding: 0 2px;
}
.todo:hover .remove {
  display: inline-block;
}
.text {
  border: none;
  outline: none;
  width: 100%;
}
.completed .text {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>
