<template>
  <div class="card add">
    <div class="cb-container">
      <button id="add-btn" @click="addTodo">+</button>
    </div>
    <div class="txt-container">
      <label for="addt">افزودن </label>
      <input
        v-model="titleTodo"
        @keypress.enter="addTodo"
        type="text"
        class="txt-input"
        placeholder="افزودن وظیفه جدید..."
        spellcheck="false"
        autocomplete="off"
        id="addt"
        dir="rtl"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddCard',
  emits:['AddNewTodo'],
  data() {
    return {
      titleTodo: '',
    };
  },
  methods: {
    addTodo() {
      this.$emit('AddNewTodo', this.titleTodo);
      this.titleTodo = '';
    },
  },
};
</script>

<style>
</style>