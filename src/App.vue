<template>
  <div>
    <h2 class="done">Todo list</h2>
    <ul>
      <TodoItem
        v-for="todo in todos"
        v-bind:todo="todo"
        v-bind:key="todo.id"
        v-on:toggle="toggle"
        v-on:remove="remove"
      />
    </ul>
    <TodoForm
      v-on:add="add"
      v-on:toggle-all="toggleAll"
      v-on:remove-all="removeAll"
    />
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component'
  import TodoForm from './TodoForm.vue';
  import TodoItem from './TodoItem.vue';


  interface Todo {
    text: string;
    done: boolean;
    id: number;
  }

  @Component({
    components: {
      TodoForm,
      TodoItem
    }
  })
  export default class App extends Vue {
    public currentId: number = 0;
    public todos: Array<Todo> = [{ text: 'buy milk', done: false, id: 0 }];

    private findTodo(id: number): { idx: number, todo: Todo } {
      const idx = this.todos.findIndex((todo: Todo) => todo.id === id);
      const todo = this.todos[idx];
      return { idx, todo }
    }

    public add(text: string): void {
      this.todos.push({
        text,
        done: false,
        id: ++this.currentId,
      });
    }

    public toggle(id: number): void {
      const { idx, todo }: { idx: number, todo: Todo } = this.findTodo(id);
      if (todo) {
        todo.done = !todo.done;
        Vue.set(this.todos, idx, todo);
      }
    }

    public remove(id: number): void {
      const { idx }: { idx: number } = this.findTodo(id);
      if (idx >= 0) {
        this.todos.splice(idx, 1);
      }
    }

    public toggleAll(): void {
      const undoneExist = this.todos.some((todo: Todo) => !todo.done);
      let todos: Todo[];
      if (undoneExist) {
        todos = this.todos
          .map((todo: Todo) => {
            if (!todo.done) {
              todo.done = true;
            }
            return todo;
          })
      } else {
        todos = this.todos
          .map((todo: Todo) => {
            todo.done = false;
            return todo;
          })
      }
      this.todos = todos;
    }
    public removeAll(): void {
      this.todos = [];
    }

  }
</script>

<style lang="scss" scoped>
  .done {
    color: red;
  }
</style>