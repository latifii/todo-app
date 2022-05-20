<template>
  <li class="card" draggable="true">
    <div class="cb-container">
      <input
        type="checkbox"
        class="cb-input"
        :checked="todo.isComplete ? true : false"
        @click="changeCheck"
      />
      <span class="check"></span>
    </div>
    <p class="item" v-if="todo.isComplete === false">{{ todo.title }}</p>
    <del class="item" v-else>{{ todo.title }}</del>
    <button class="clear" @click="removeTodo">
      <img src="@/assets/images/icon-cross.svg" alt="Clear it" />
    </button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todo'],
  emits: ['changeCheckBox', 'removeTodoList'],
  methods: {
    changeCheck() {
      this.$emit('changeCheckBox', this.todo.id, !this.todo.isComplete);
    },
    removeTodo() {
      this.$emit('removeTodoList', this.todo.id);
    },
  },
};
</script>

<style>
</style>