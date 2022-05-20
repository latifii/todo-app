/* eslint-disable vue/return-in-computed-property */
<template>
  <base-header></base-header>
  <main>
    <add-card @AddNewTodo="newTodo"></add-card>
    <ul class="todos">
      <todo-item
        v-for="activity in getTodo"
        :key="activity.id"
        :todo="activity"
        @changeCheckBox="changeStatus"
        @removeTodoList="removeTodo"
      ></todo-item>
    </ul>
    <div class="card stat">
      <p class="corner">
        <span id="items-left">{{ overTodo }}</span> مورد باقی مانده
      </p>
      <div class="filter">
        <button
          id="all"
          :class="{ on: activeTab === 'all' }"
          @click="changeTab('all')"
        >
          همه
        </button>
        <button
          id="active"
          :class="{ on: activeTab === 'active' }"
          @click="changeTab('active')"
        >
          فعال
        </button>
        <button
          id="completed"
          :class="{ on: activeTab === 'completed' }"
          @click="changeTab('completed')"
        >
          تکمیل
        </button>
      </div>
      <div class="corner">
        <button id="clear-completed" @click="todoRemoveAllDone">
          حذف تکمیل شده ها
        </button>
      </div>
    </div>
  </main>
  <base-footer></base-footer>
</template>

<script>
import BaseHeader from './components/BaseHeader.vue';
import BaseFooter from './components/BaseFooter.vue';
import AddCard from './components/AddCard.vue';
import TodoItem from './components/TodoItem.vue';

export default {
  name: 'App',
  components: { BaseHeader, BaseFooter, AddCard, TodoItem },
  data() {
    return {
      activities: [
        { id: 1, title: 'آموزش JS', isComplete: false },
      ],
      activeTab: 'all',
    };
  },
  computed: {
    overTodo() {
      return this.activities.filter((item) => item.isComplete === false).length;
    },
    // eslint-disable-next-line vue/return-in-computed-property
    getTodo() {
      switch (this.activeTab) {
        case 'all':
          return this.activities;

        case 'active':
          return this.activities.filter((item) => item.isComplete === false);

        case 'completed':
          return this.activities.filter((item) => item.isComplete === true);
        // default:
        //   return this.activities;
      }
    },
  },
  methods: {
    newTodo(title) {
      const newActivity = { id: Math.random(), title, isComplete: false };
      this.activities.push(newActivity);
      console.log(newActivity);
      console.log(this.activities);
    },
    changeStatus(id, status) {
      let newActivitis = [...this.activities];
      const selectedTodo = newActivitis.find((item) => item.id === id);
      selectedTodo.isComplete = status;
      this.activities = newActivitis;
    },
    removeTodo(id) {
      this.activities = this.activities.filter((item) => item.id !== id);
    },
    todoRemoveAllDone() {
      let newActivitis = [...this.activities];
      const removeDoneTodo = newActivitis.filter(
        (item) => item.isComplete === false
      );
      this.activities = removeDoneTodo;
    },
    changeTab(tab) {
      this.activeTab = tab;
    },
  },
};
</script>

<style>
</style>