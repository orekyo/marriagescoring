<template>
  <div>
    <a href="https://note.com/koseidaiki/n/nb7df493af9a6" target="_blank">
      <img src="./assets/favicon.png" class="logo" alt="俺の嫁探し" />
    </a>
  </div>
  <SpecInputForm />
</template>

<script setup>
import SpecInputForm from './components/SpecInputForm.vue'
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
