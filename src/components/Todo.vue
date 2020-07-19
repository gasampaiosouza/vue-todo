<template>
  <main class="todo">
    <input
      class="list-input"
      type="text"
      v-model="todoInput"
      @keyup.enter="addTodo"
      placeholder="I need to..."
    />

    <p class="desc" style="margin-bottom: 0">To mark as done, just click it!</p>
    <p class="desc">you can delete notes by right clicking it too.</p>

    <div class="list">
      <div
        :class="{ done: todo.done }"
        class="list-item"
        v-for="todo in todos"
        @click="complete(todo)"
        @contextmenu="deleteTodo($event, todo)"
        :key="todo"
      >
        <p class="item-title">{{ todo.title }}</p>
        <span @click="deleteTodo($event, todo)" class="close-icon">&times;</span>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todoInput: "",
      todos: [
        {
          title: "Your first todo item!",
          done: false
        }
      ]
    };
  },
  methods: {
    addTodo() {
      const capitalize = string =>
        string.charAt(0).toUpperCase() + string.slice(1).toLowerCase();

      this.todos.push({
        title: capitalize(this.todoInput),
        done: false
      });

      this.todoInput = "";
    },
    complete(todo) {
      return (todo.done = !todo.done);
    },
    deleteTodo(event, todo) {
      event.preventDefault();
      const index = this.todos.indexOf(todo);

      return this.todos.splice(index, 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "./style.css";
</style>
