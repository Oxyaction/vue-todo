<template>
  <transition name="fade">
    <li v-bind:class="{done: todo.done}">
      <label>
        <input
            type="checkbox"
            v-bind:checked="todo.done"
            v-on:change="$emit('toggle', todo.id)"
        >
        {{ todo.text }}
      </label>
      <button @click="$emit('remove', todo.id)">X</button>
    </li>
  </transition>
</template>

<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component'

  @Component({
    props: {
      todo: {
        type: Object,
        required: true,
      }
    }
  })
  export default class TodoItem extends Vue {}
</script>

<style lang="scss" scoped>
  .done {
    text-decoration: line-through;
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .2s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
</style>