<template>
  <div>
    <input
      v-bind:class="{error: isError}"
      type="text"
      v-model="text"
      placeholder="todo text"
      v-on:keydown.enter="add"
      v-on:keydown="isError = false"
    />
    <button v-on:click="add">
      Add
    </button>
    <div v-if="isError" class="error-text">todo target should not be empty</div>
    <div>
      <button @click="$emit('toggle-all')">
        Done all
      </button>
      <button @click="$emit('remove-all')">
        Remove all
      </button>
    </div>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component'

  @Component
  export default class TodoForm extends Vue {
    text: string = '';
    isError: boolean = false;

    add() {
      if (this.text.trim() === '') {
        this.isError = true;
      } else {
        this.$emit('add', this.text.trim());
        this.text = '';
      }
    }
  }
</script>

<style lang="scss">
  .error {
    border: 1px solid red;
  }

  .error-text {
    color: red;
  }
</style>