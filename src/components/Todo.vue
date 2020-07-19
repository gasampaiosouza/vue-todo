<template>
  <main class="container">
    <input type="text" v-model="todoInput" @keyup.enter="addTodo" placeholder="I need to do..." />

    <div
      class="card"
      v-for="todo in todos"
      @click="complete(todo)"
      @contextmenu="deleteTodo($event, todo)"
      :key="todo"
    >
      <div class="card-body" :class="{ done: todo.done }">{{ todo.title }}</div>
    </div>

    <!-- <ul>
      <li
        v-for="todo in todos"
        @click="complete(todo)"
        @contextmenu="deleteTodo($event, todo)"
        :key="todo"
      >
        <p :class="{ done: todo.done }">{{ todo.title }}</p>
      </li>
    </ul>-->
  </main>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todoInput: "",
      todos: []
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.todoInput,
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
</style>
