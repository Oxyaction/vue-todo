<template>
  <div>
    <ul>
      <li v-for="todo in todos">
        {{todo.text}}
      </li>
    </ul>
    <TodoForm v-on:add="add"/>
  </div>
</template>

<script>
  import TodoForm from './TodoForm.vue';
  export default {
    data: () => ({
      todos: [{ text: 'buy milk', done: false }]
    }),
    components: {
      TodoForm
    },
    methods: {
      add(text) {
        this.todos.push({ text, done: false });
      }
    }
  };
</script>