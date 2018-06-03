<template>
  <div>
    <input
      type="text"
      v-model="text"
      placeholder="todo text"
      v-on:keydown.enter="add"
    />
    <button v-on:click="add">
      Add
    </button>
  </div>
</template>

<script>
  export default {
    data: () => ({
      text: ''
    }),
    methods: {
      add() {
        this.$emit('add', this.text);
        this.text = '';
      }
    }
  }
</script>