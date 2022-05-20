<template>
  <header class="card">
    <h1>لیست وظایف</h1>

    <button id="theme-switcher" @click="changeTheme">
      <img
        :src="sunIcon"
        alt="Change color theme"
        v-if="defaultTheme === 'dark'"
      />
      <img :src="moonIcon" alt="Change color theme" v-else />
    </button>
  </header>
</template>

<script>
import sun from '../assets/images/icon-sun.svg';
import moon from '../assets/images/icon-moon.svg';
export default {
  name: 'BaseHeader',
  data() {
    return {
      sunIcon: sun,
      moonIcon: moon,
      defaultTheme: 'dark',
    };
  },
  methods: {
    changeTheme() {
      if (this.defaultTheme === 'dark') {
        this.defaultTheme = 'light';
        document.querySelector('body').classList.add('light')
      } else {
        this.defaultTheme = 'dark';
        document.querySelector('body').classList.remove('light')
      }
    },
  },
};
</script>

<style>
</style>