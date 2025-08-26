<script>
import NotesList from "./components/NotesList.vue";

export default {
  name: "App",
  components: {
    NotesList,
  },
};
</script>

<template>
  <div id="app">
    <NotesList />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

</style>
